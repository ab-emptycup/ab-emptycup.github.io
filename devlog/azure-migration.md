---
layout: page
title: Migrating azure deployment
---

Due to some administrative constraints, I'm having to migrate our cloud deployment across azure subscriptions.
This is a log of that effort.
<br><br>

## November 2

- Recieved a feasibility and cost estimate of the migration.
- Finished a call with Xencia (MS CSP). Migration seems simple and straight forward, mostly without downtime.
- Shared Global Administrator access to Xencia for both subscriptions.
- Awaiting their confirmation for timings for migration. Likely in the next 2 days.
- The migration has been scheduled for next Friday 6am.

## November 4

Got on the call for the migration at 6am

TODO: Before beginning all the the available resource providers were "registered" for the new subscription. But, those registrations have not been evoked after the migration. This needs to be double checked.

- We first moved the target subscription to the source directory / tenant. Moved the resources to the target subscription and then moved the target subscription back to the target tenant.
- We had a road block moving the studio render workers. Apparently moving spot instances across subscriptions is not currently supported. So, we decided to just move the VHD snapshot to the new subscription and create new worker VMs again.
- Next we moved the app services. We deleted the SSL bindings and the app certificates first. Then created them again after the move. Remembered that studio3d backend doesn't have a custom domain configured.
- We then created a new SSH key in the new subscription as moving SSH keys is not supported.

After the migration, I successfully created a render worker VM with a dynamic ip on the new subscription. But, I realised that there is an issue with the hardcoded azure credentials in the app. Till the app env var config is updated, the app will still try to spin up render workers from the old subscription. Further, the render-worker script itself needs to be updated with new tenent credentials for it to be able to turn itself off.

I have left these changes for a future session as there seem to be some active render work happening on the product and I don't want to disrupt that. I will mostly likely get to it during the first half of the next week.
There is also the task of migrating s3 assets to azure. It also looks like I should document things even for studio3d. I don't think I'll remember all the important things if I come back after a month or two. At this point, I'm not confident that I don't have to come back for a couple of months.


## November 8

- Created spotVMs in the new subscription.
- Created a service principal in azure to let the app spin up the new spotVMs. Got stuck for an hour fixing broken permissions on the newly created SP.
- Realised we have quote for upto 4 worker VMs in each region. But, failed to create workers because location move is not supported for VHD snapshot. Move was not even supported for spot vm instance. This is something I need to check with Xencia.
- Spent another hour trying to figure out why preemptible machines are not being started when a render request comes in. Turned out I forgot to set the appropriate preemptible tag on instances.
- Confirmed that catalogue3d doesn't require any config update due to the migration.

----
<br>


## November 21:

There are a few tasks pending from the azure subscription migration:

- Review and deallocate assets from the old subscription.
- Copy the _render-worker-vhd_ snapshot into a storage account and create duplicate machines in other regions.
- Resolve the permissions issue with SSH into app service in new subscription.

Apart from that, there is another major change. All the cloud assets currently deployed in s3 need to be migrated to Azure Blob Storage. That would save us a big AWS bill. I'm planning to start work on this. These assets are being used by
the production deployment. That adds some complexity.

1. Write an Azure backed _Store_ class in the _emptycup3d_ backend.
2. Create a storage account on Azure for _emptycup3d_.
3. Copy assets from s3 to the newly created storage account.
4. Ensure _emptycup3d_ is working with the Azure backed _Store_ connected to the _emptycup3d_ storage account.
5. Copy all the assets from s3 to the _studio3d_ storage account.
6. Setup a "test" deploy for the _studio3d_ app service and deploy the changes there.
7. Ensure _studio3d:dev_ is working smoothly.
8. Deploy the update to _studio3d:prod_.



