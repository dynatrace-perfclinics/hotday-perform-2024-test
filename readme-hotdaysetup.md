# This is for setting up a new HOTDAY for Dynatrace HOTDAY Labs

## 1: Create the new GitOps Platform Definition in this Git Repo

The tutorial will launch a platform based on the definition on a public git repository. We are using this github repo but we need a new folder for each classroom as each classroom will get its own unique domain URL as well as uses its own Dynatrace Environment. 
Hence we have to create a new folder and replace some PLACEHOLDERs

1: Create a copy of the gitops directories and give it a meaningful *CLASSROOM_ID*, e.g: gitops_hotday_uk
2: replace the following placeholders:
- BASE_DOMAIN_PLACEHOLDER with the hotday domain, e.g: https://dtulab1234567890.dynatrace.training
- DT_TENANT_LIVE_PLACEHOLDER with the dynatrace live domain name, e.g: abc12345.sprint.dynatracelabs.com
- FORKED_REPO_GITOPS_CLASSROOMID_PLACEHOLDER with the classroom name you used for the gitops directory, e.g: gitops_hotday_uk
- FORKED_TEMPLATE_REPO_PLACEHOLDER with the URL of this repo, e.g: https://github.com/dynatrace-perfclinics/hotday-perform-2024-test
3: Commit the new directory back to this github repository

## 2: Create the platform using the DT University Bastion Host

Every HOTDAY has its own bastion host that is already connected with the K8s cluster as well as has all environment variables set correct.y

1: Login to your DT University bastion host
2: sudo vi /etc/environment --> validate that all values are correct and CHANGE FORKED_REPO_GITOPS_CLASSROOMID to your *CLASSROOM_ID*, e.g: gitops_hotday_uk
3: 