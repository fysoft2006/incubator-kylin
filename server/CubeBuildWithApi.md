## Build Cube with Kylin Api

### 1.	Login
* 	POST http://kylin.corp.ebay.com/kylin/api/user/authentication
* 	Currently, kylin uses [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).
* 	After auth, client should go f ollowing requests with cookies. 

### 2.	Get the specified cube. 
* 	GET http://kylin.corp.ebay.com/kylin/api/cubes?cubeName=clsfd_ga_cube_dayweek&limit=15&offset=0. 
* 	Client can find cube data date ranges in segments information of the cube detaill.

### 3.	Then submit a build job of the cube. 
* 	PUT http://kylin.corp.ebay.com/kylin/api/cubes/clsfd_ga_cube_dayweek/rebuild. For put request body detail please refer to service doc. 
*         StartTime and endTime should be utc timestamp.
* 	This method will return a newly created job instance, in which the uuid is the identity of job to track job status.

### 4.	Track job status. 
* 	GET http://kylin.corp.ebay.com/kylin/api/jobs/1421ea52-d15e-480c-9983-e0549e386bf6
* 	job_status represents current status of job.

### 5.	If the job failed, you can resume the job. 
* 	PUT http://kylin.corp.ebay.com/kylin/api/jobs/1421ea52-d15e-480c-9983-e0549e386bf6/resume