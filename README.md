# S3 Object Lock - WORM Storage
1. Create a new Bucket
		- Enable Object Lock
		- Enable Versioning
		- Enable Default Encryption
2. Object lock can be configured with retention period or default period at the time of ingestion. 
	- Ways of managing retention of an object in S3
		- Retention period - Locked for defined period and can't be deleted or updated for that period
		- Legal Hold - Its same as Retention period but with No unlimited period until you delete it explicitly. 
		- Objects can have both but not neither. 
	- Key things while ingesting Objects 
		- It works on versions only. In case you try to override the object with the same key it will create an another version and older version will remain there as per the retention defined on ingestion. 
	- Retention Modes in S3
		- Governance mode:  in this mode it will not allow delete until you have specific permission to delete the object version.  There is an option to delete object or alter retention if required. 
		- Compliance mode:  a WORM object version will not be deleted in this mode. Its majorly used for Compliance requirement like regulatory recordkeeping. 
		- 
		  


3. POC via AWS CLI to store documents for compliance requirement in compliance mode with specific retention period. 
	- Put Object with retention period
		- aws s3api put-object --bucket s3objectlock-worm --key worm/test.txt --body test.txt --object-lock-mode COMPLIANCE --object-lock-retain-until-date 2020-10-03
		- 
		- ETag and version details on S3 object - 
		- 
		- Reading the WORM object version - 
		- aws s3api get-object --bucket s3objectlock-worm  --key worm/test.txt --version-id UEsrdn1oMEICF0fvwwXsDpj8a2tvReZ4
		- 
		- It means to get the accurate version of object we also need to store the object version Id with object key in client API. 
	- Object Lock with Lifecycle rules
		- 
		  

3. How to enable object Lock on existing bucket?
	- you can not enable object lock from aws console own your own. Contact AWS support and they will do it for you manually. 
