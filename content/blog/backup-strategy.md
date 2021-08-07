---
Title:  Backup Strategy for Website & Cloud Data
Template: blog-content
Description: After a few bouts of data-loss, I venture into the realm of data backups! The goal: Automatic, Encrypted incremental backups that push to a secondary cloud storage provider...
Author: Tim White
Date: 2020-08-07
Robot: noindex,nofollow
Tags: [technical,website,backups,bash,rsync,cron]
---

# Backup Strategy for Website & Cloud Data

![Image of Server with Storage Drive Array](https://cloud.timwhite.io/s/HziRfqXenoBQnrN/preview)

## Introduction
Unlike with Google, Apple, Amazon, and Microsoft, if you host your own data, you are at a heightened risk of data-loss without a proper backup solution.

If you use solid-state drives for your storage volumes, your data will be more secure [from a drive failure perspective](https://www.backblaze.com/blog/how-reliable-are-ssds/) than more traditional hard-disk drives, but you never know when a corrupted or infected file may compromise everything.

A simple example of this happened to me recently. It was business as usual: I was [editing this website over sFTP](https://atom.io/packages/sftp-deployment) through my preferred text editor, [Atom](https://atom.io/). Somehow, the data was corrupted during upload, and I ended up losing a few hours of work.

This ended up having a positive effect on my cloud hosting, as I was finally motivated to implement a reliable data backup system!

See my [Data Backup Wiki](https://wiki.timwhite.io/data_backup_solution) for specific examples of the backup and upload scripts I'm using as a result of this post!

## Which Data to Backup
What information do you care enough about to pay someone to store a backup of?

Digital photo albums are a common example of data considered valuable to those without printed backups. Similarly, if you store personal and professional technical documents in place of hard-copies, you may also consider that data of high value. I have both of these to worry about.

Configuration & setup files that exist on the server are less important when compared to the cost of backing them up. I can always reinitialize the [base server (Ubuntu)](https://ubuntu.com/), [Nginx web server](https://nginx.org/en/), and [the cloud apps](https://timwhite.io/updates/self-hosted-cloud-server) associated with [TimWhite.io](https://timwhite.io/), but the content I create and store would be much harder to recreate.

I have chosen to backup my main data drive (fileserver), Nginx configuration files, and my website's root directory.

## Copy Count
While many follow the [3-2-1 approach to backups](https://www.carbonite.com/blog/article/2016/01/what-is-3-2-1-backup/), others may feel comfortable with the risk level associated with maintaining fewer copies of their data. You will need to determine your comfort level and adjust your backup strategy accordingly.

I estimate that if the failure rate for any given solid-state drive is already low, then the combined probability of that solid-state drive and one backup failing would be suitable. Depending on your backup method and number of copies, you can mitigate the risk of an infected or corrupted file being propagated into all copies of your data.

## Backup Locations
One thing that you should know at this point is that there is a chance that all data housed on a single server is susceptible to a single failure.

For this reason, many choose to locate at least one backup copy off-site. There are two main ways to accomplish this: push the files to another cloud server or store them through [object- or block-storage](https://cloudian.com/blog/object-storage-vs-block-storage/) providers like [Amazon S3, Backblaze B2, Azure etc.](https://www.cloudwards.net/azure-vs-amazon-s3-vs-google-vs-backblaze-b2/).

## Cost of Backup Solution
As I covered in my Self-Hosted Cloud Server post, my two main goals for cloud app related projects are to keep costs low, and to do as much back-end development as possible.

Because of this, I would like to ensure the solution I implement is scalable so I can start with a low-cost/low-size backup and expand when necessary.

Paid software services that accomplish these types of backup solutions exist, like [Carbonite](https://www.carbonite.com/), [CrashPlan](https://www.crashplan.com/en-us/), [Backblaze Online Backup](https://www.backblaze.com/cloud-backup.html), etc., and typically range from a fixed cost of $5 to $10 USD/month.

While some of these services offer unlimited data for backups, the volume of data I currently need to backup is small enough that it would be cheaper to go with a pay-by-the-gigabyte solution.

Since my server is headless, I will also need shell access to control the backups, where most of these paid software suites are GUI-focused.

At present, I have about 100 gigabytes of raw data in need of backups, and I estimate that will likely expand by around 12 GB per year (1 GB/month) moving forward.

Let's start with a cost comparison per-gigabyte of block-storage across popular providers. I'm sure there are many other providers, but I have only included four of the most popular for this comparison.

### Simple cost comparison

|Provider                                                               |Storage ($/GB/Month)  |Download ($/GB)|
|-----------------------------------------------------------------------|----------------------|---------------|
|[Backblaze B2](https://www.backblaze.com/b2/cloud-storage.html)        |$0.005                |$0.01          |
|[Microsoft Azure](https://azure.microsoft.com/en-us/services/storage/) |$0.018                |$0.087         |
|[Google Cloud](https://cloud.google.com/storage/)                      |$0.020                |$0.12          |
|[Amazon S3](https://aws.amazon.com/s3/)                                |$0.021                |$0.09          |

Summary: At a quick glance, Backblaze B2 provides the cheapest cloud storage. Let's dig into this a bit deeper.

### Expanded cost comparison

|Assumptions       |     Size  |
|------------------|----------:|
|Initial Upload:   |    100 GB |
|Monthly Upload:   |      1 GB |
|Monthly Download: |      1 GB |

|                            |  Backblaze B2 |  Microsoft Azure | Google Cloud | Amazon S3 |
|----------------------------|--------------:|-----------------:|-------------:|----------:|
|Initial Upload Cost *:        |   $0.50       |  $1.80           | $2.00        | $2.10     |
|Monthly Upload Cost:        |   $0.01       |  $0.02           | $0.02        | $0.02     |
|Monthly Download Cost:      |   $0.01       |  $0.09           | $0.12        | $0.09     |
|Total Monthly Cost:         |   $0.56       |  $2.00           | $2.25        | $2.33     |
|Total Cost 12 months:       |   $6.50       |  $24.05          | $27.00       | $27.90    |

\* The recurring monthly cost for the initial sum of data.

This is a very high-level comparison, and I haven't given too much attention to advanced topics like Glacier/frozen storage for further discounted pricing.

I have used Backblaze, Amazon, and Google Cloud across various projects in the past. Amazon has a particularly complex cost schedule, and Google Cloud is clearly expensive. I have no familiarity with Azure, but as it stands, there is a clear winner.

Backblaze has an excellent web interface, offers API access, and appears to be the cheapest option by a large margin. For these reasons I have selected Backblaze as my data storage provider!

## Server-Side Backup Methods
When dealing with a basic file server including a series of directories, sub-directories, and files, there are a few ways to take backups.

Today I'll briefly introduce the following three backup types, and detail which is most suitable for my requirements.

### Full
Full backups are the most straight forward and least practical. A plain carbon copy is made of the top level directory that includes the existing folder structure and all nested files.

The result is an identical clone of the data, with an identical total file count and size. To store this backup off-site (cloud storage) will require uploading the entire file-system every time a backup is created. This could incur a huge cost depending on the size of the backup and storage provider.

Additionally, frequent generations of full backups stresses the local storage drive as tens- or hundreds of gigabytes are constantly deleted and rewritten with each backup.

For large file systems, full backups can take hours or even days to complete which is a limit in itself in terms of how frequently you can take backups.

### Incremental

Incremental backups involve only making copies of the data that has changed since the most-recent backup. A full backup is taken initially, and subsequent partial backups are stored up until the time of restoration.

This method of backups allows the user to reduce the amount of required storage space, limit the stress on the local storage drive, and dramatically increase the speed of performing a backup compared to full backups.

The technical implementation of this method typically involves checking each file and folder's attributes including "last modified" and comparing them to the timestamp of the last incremental backup. If the modified date was after the backup, the file is copied; If before, the file is skipped.

During recovery, the full backup and all subsequent partial backups are restored sequentially in order to provide the most up to date data.

One limitation of incremental backups is that deletions are not accounted for. All file deletions must be either propagated manually, or intentionally allowed and ignored in the backups.

For the purposes of my backups (recovery from catastrophic events), I feel comfortable in allowing deletions to exist in backup form.

For individuals with large amounts of data and large quantities of deleted files, there may be a significant cost benefit to keeping track of deletions and propagating them manually, or switching to a different backup method.

### Differential
Differential backups are widely similar to Incremental backups, except instead of comparing timestamps to the latest partial/incremental backup, the timestamps are compared to the last full backup.

The main benefit here is that instead of needing to restore all partial backups sequentially, the full backup and single differential backup can be restored. This helps users of larger backups that have requirements of faster restore times.

I don't have such a time requirement, so I have opted for a solution that utilizes incremental backups.

## Encryption, Automation, Software, and Scheduling

Enter [Rclone, Borg, and Cron](https://wiki.timwhite.io/data_backup_solution)
