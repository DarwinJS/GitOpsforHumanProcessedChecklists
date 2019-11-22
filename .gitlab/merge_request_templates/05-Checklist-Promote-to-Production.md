
Name The New Issue Like This (substitute changeset verson): Promote Changeset v4.3 To Production

### Overview Details
_______
Promotion Date: `_REPLACE_WITH_ YYYY-MM-DD`
Checklist Completer(s): `_REPLACE_WITH_ @MentionHandle(s)`
Changeset Version: `_REPLACE_WITH_ X.Y`
Stack ID for prechange Blue Stack: `_REPLACE_WITH_ STACKID`
Stack ID for prechange Green Stack: `_REPLACE_WITH_ STACKID`
Changeset Deployment Attempt Result (NO GO, SUCCEEDED, FAILED): `_REPLACE_WITH_ NO GO or SUCCEEDED or FAILED`

### Notify and Subscribe
Could the following individuals please acknowledge they are aware of this merge request:

#### Auditors / Listeners
Please check off your name to acknowledge you know of this issue and have subscribed to it:
* [ ] `_REPLACE_WITH_@PersonalName1`
* [ ] `_REPLACE_WITH_ @PersonalName2`

#### Changeset Team Acknowledgements
Please check off your name to acknowledge you know of this issue and have subscribed to it:
* [ ] `_REPLACE_WITH_ @PersonalName4`
* [ ] `_REPLACE_WITH_ @PersonalName4`
* [ ] `_REPLACE_WITH_ @PersonalName4`

/cc `_REPLACE_WITH_ @ProductionChangesetGroup`


### Pre-Flight (5 Days Before)
* [ ] Confirm Go Call
* [ ] Confirm Maintenance Window Schedule and Record here: _MAINTENANCE_WINDOW_DATE_TIME_

### Phase 1: Change Preparation (T-4hrs before change)
1. * [ ] At T-4hrs - Kick-off special pre-change backup
    1. * [ ] In backup system, select "Production Pre-change Backup Routine"
    2. * [ ] Name it "Production Pre-changeset `_REPLACE_WITH_ X.Y` Backup"

### Phase 2: PreChange Commencement Notice (1 minute before change)
1. * [ ] Post changeset commencement announcement
   "Changeset `_REPLACE_WITH_ X.Y` is commencing to the Production environment for the Andromeda system."
   1. * [ ] Email List "Andromeda PreProduction Watch"
   2. * [ ] Slack channel "Andromeda PreProduction Watch"
   3. * [ ] Status at "status.andromeda.abccorp.com"

### Phase 3: Begin Rolling Container Updates (1 minute before change)
1. * [ ] Ensure that you are operating on the current Blue stack by verifying the ID at the top of this checklist.
2. * [ ] On CloudFormation "IaC Production Stack" Update the following parameters
   1. * [ ] ContainerVersion: _NEW_CONTAINER_VERSION_
3. * [ ] Submit CloudFormation stack "IaC Production Stack"
4. * [ ] Monitor for completion, check this AFTER item when update is complete to properly record elapsed time of the automation.

### Phase 4: Test Blue Stack and Make GO/NO GO Decision
1. * [ ] Test Blue side of production by creating and completing an issue with template "Blue-side-tests-production" and record issue number in the following (to map the test checklist to this merge request):
Closes #_ISSUE_NUMBER_
2. * [ ] Make Go/No Go Decision and send notification on decision.
   "We are a `_REPLACE_WITH_ GO or NO_GO` on updating the Production stack"
   1. * [ ] Email List "Andromeda PreProduction Watch"
   2. * [ ] Slack channel "Andromeda PreProduction Watch"
   3. * [ ] Status at "status.andromeda.abccorp.com"

> Note one of the below sections can be deleted when it is not the chosen course of action.

### Phase 5: GO Decision
1. * [ ] Prescale Blue side
   1. * [ ] Open the Ec2 Console
   2. * [ ] Manually update the AWS ASG to scale it to the current size of the green side
   3. * [ ] Monitor for completion, check this AFTER item when update is complete to properly record elapsed time of the automation.
2. * [ ] Update DNS in console:
   1. * [ ] Open the AWS Route53 Console
   2. * [ ] Find the record for andromeda.abccompany.com and switch the load balancer to the current Blue Stack ID (at top of checklist)
3. * [ ] Run post cutover automated testing.
4. * [ ] If tests failed, check this step and go forward to section "Phase 5: NO GO Decision / Backoff Failed Attempt"
5. * [ ] If tests pass, In "Changeset Deployment Attempt Result" at the top of this checklist record "SUCCEEDED"

### Phase 5: NO GO Decision / Backoff Failed Attempt
1. * [ ] If changeset was a NO GO, in "Changeset Deployment Attempt Result" at the top of this checklist record "NO GO"
2. * [ ] If changeset failed, in "Changeset Deployment Attempt Result" at the top of this checklist record "FAILED"

### Phase 6: Post Change Wrap Up
1. * [ ] If Changeset promotion was successful, post:
   "Changeset `_REPLACE_WITH_ X.Y` was successfully deployed to the Production environment for the Andromeda system."
   1. * [ ] Email List "Andromeda PreProduction Watch"
   2. * [ ] Slack channel "Andromeda PreProduction Watch"
   3. * [ ] Status at "status.andromeda.abccorp.com"
2. * [ ] If Changeset promotion failed:
   1. * [ ] After updating with version and either "failure" or "no-go", post message "Changeset `_REPLACE_WITH_ X.Y` _failed_or_was a no-go_ to deploy to the Production environment for the Andromeda system." to
      1. * [ ] Email List "Andromeda PreProduction Watch"
      2. * [ ] Slack channel "Andromeda PreProduction Watch"
      3. * [ ] Status at "status.andromeda.abccorp.com"
   2. * [ ] Creating and complete evidence section an issue with template "Changeset Failure Post Mortem Report for Changeset `_REPLACE_WITH_ X.Y`" and record issue number in the following (to map the test checklist to this merge request):
   Post mortem issue: `_REPLACE_WITH_ #ISSUE_NUMBER`

### Phase 6: Closing Out This Issue
* [ ] If the change succeeded, close this checklist after success is verified.
* [ ] If the change failed, close this checklist after post-mortem is complete.