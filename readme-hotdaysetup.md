# This is for setting up a new HOTDAY for Dynatrace HOTDAY Labs

Infos on regional HOTDAYS and their domains
|| Location || domain || classroom_id || 
| Dry Run (Apr 4) | dtulab462102617 | gitops_dryrun_hot_emea |
| Maidenhead |  dtulab446565966 | gitops_emea_uk | https://blx54279.sprint.dynatracelabs.com
| Utrecht | dtulab447946107 | gitops_emea_nl |
| Frankfurt | dtulab454101030 | gitops_emea_de |
| Rome (ITR10) | dtulab448873578 | gitops_emea_itr |

## 1: Create the new GitOps Platform Definition in this Git Repo

The tutorial will launch a platform based on the definition on a public git repository. We are using this github repo but we need a new folder for each classroom as each classroom will get its own unique domain URL as well as uses its own Dynatrace Environment. 
Hence we have to create a new folder and replace some PLACEHOLDERs

1: Create a copy of the gitops directories and give it a meaningful *CLASSROOM_ID*, e.g: gitops_emea_uk
2: replace the following placeholders:
- BASE_DOMAIN_PLACEHOLDER with the hotday domain, e.g: dtulab1234567890.dynatrace.training
- DT_TENANT_LIVE_PLACEHOLDER with the dynatrace live domain name, e.g: https://abc12345.sprint.dynatracelabs.com
- FORKED_REPO_GITOPS_CLASSROOMID_PLACEHOLDER with the classroom name you used for the gitops directory, e.g: gitops_emea_uk
- FORKED_TEMPLATE_REPO_PLACEHOLDER with the URL of this repo, e.g: https://github.com/dynatrace-perfclinics/hotday-perform-2024-test
- GEOLOCATION_PLACEHOLDER with the correct GEO Location, e.g: GEOLOCATION-3F7C50D0C9065578
3: Commit the new directory back to this github repository

## 2: Create the platform using the DT University Bastion Host

Every HOTDAY has its own bastion host that is already connected with the K8s cluster as well as has all environment variables set correct.y

1: Login to your DT University bastion host
2: sudo vi /etc/environment --> validate that all values are correct and CHANGE FORKED_REPO_GITOPS_CLASSROOMID to your *CLASSROOM_ID*, e.g: gitops_emea_uk
3: now run ./deploy-steps-1-5.sh and wait until ArgoCD and GitLab is up and Running!

Once its done you can run: ./printenvdetails.sh

## 3: Create PAT for GitLab

1. open your GitLab UI and navigaet to the Personal Access Token Page --> https://gitlab.dtulabxxxxxxxxx.dynatrace.training/-/user_settings/personal_access_tokens
2. Create a new token with api, read_repository and write_repository
3. take this PAT value and specify it in /etc/environment in GL_PAT

## 4: Finish Platform Installation with step-6

Now run ./deploy-step-6.sh

## 5: Restart ArgoCD App Set Controller

kubectl delete pod -n argocd argocd-applicationset-controller-xxxxxxxxxxxxx

## 6: Finish Dynatrace Configuration

Couple of things in Dynatrace
1: Make sure new K8s Experience is enabled, that K8s monitoring includes events & prometheus and that AppSec Vulnerability Detection is Enabled!
2: Import the Notebooks and Dashboards for the HOTDAY and share them with all attendees from /dynatraceassets
3: Edit the links in the HOTDAY Notebook to show the correct logins
4: Import the Lifecycle Automation Workflow, give it all needed priviliges, make it public and edit the endpoint for sending messages to Backstage!
5: Add the backstage domain to the allow list for outgoing notification calls!