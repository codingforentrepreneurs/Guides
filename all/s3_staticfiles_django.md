# S3 Static & Media Files for Django

Using Amazon Web Services (AWS) S3 For storing static and media files for a Django Project.

1. **Create AWS Account**: [here](http://aws.amazon.com/)

2. **Create AWS User Credentials**
	
	1. Navigate to [IAM Users](https://console.aws.amazon.com/iam/home?#users)
	
	2. Select `Create New Users`
	
	3. Enter `awsbean` as a username (or whatever you prefer)
	
	4. Ensure `Generate an access key for each user` is **selected**.
	
	5. Select `Download credentials` and keep them safe. 
	
	6. Open the `credentials.csv` file that was just downloaded/created 

	7. Note the `Access Key Id` and `Secret Access Key` as they are needed for a future step. These will be referred to as `<your_access_key_id>` and `<your_secret_access_key>`

3. **Create new S3 Bucket**
	1. Navigate to S3 through the [Console](https://console.aws.amazon.com) or this [Link](https://console.aws.amazon.com/s3)
	2. Click `Create Bucket`
	3. Create a unique `Bucket Name` such as `your-project-bucket` or any other name you choose.
	4. Select `Region` relative to your primary users' location.
	5. Click `Create`

	Make note of the `Bucket Name` you created here. It will replace `<your_bucket_name>` below.

4. **Add Default Access Policies to your IAM User**:
	1. Navigate to the user's account such as: [https://console.aws.amazon.com/iam/home?region=us-west-2#users/awsbean](https://console.aws.amazon.com/iam/home?region=us-west-2#users/awsbean)
	2. Click on `Permissions` tab.
	3. Click on `Attach Policies` and add any policies you'd like to give this user access to.

	This step, we're not going to do. Instead, we are going to limit what our IAM User has access to in our AWS account. So onto the next step.

5. **Add Custom Permissions to your IAM User**
	1. Navigate to the user's account such as: [https://console.aws.amazon.com/iam/home?region=us-west-2#users/awsbean](https://console.aws.amazon.com/iam/home?region=us-west-2#users/awsbean)
	2. Click on `Permissions` tab.
	3. Click tab for `Inline Policies` and create a new one.
	4. Select `Custom Policy`
	5. Set `Policy Name` to `S3Django` (or any name you decide)
	6. Set `Policy Document` to, make note of the `<your_bucket_name>` as we just set this bucket name:
		```
		{
			"Statement": [
			    {
			        "Effect": "Allow",
			        "Action": [
			            "s3:ListBucket",
			            "s3:GetBucketLocation",
			            "s3:ListBucketMultipartUploads",
			            "s3:ListBucketVersions"
			        ],
			        "Resource": "arn:aws:s3:::<your_bucket_name>"
			    },
			    {
			        "Effect": "Allow",
			        "Action": [
			            "s3:*Object*",
			            "s3:ListMultipartUploadParts",
			            "s3:AbortMultipartUpload"
			        ],
			        "Resource": "arn:aws:s3:::<your_bucket_name>/*"
			    }
				]
		}
		```

	7. The `Action`s that we choose to set are based on what we want this user to be able to do. The line `"s3:*Object*",` will handle a lot of our permissions for handling objects for the specified bucket within the `Recourse` Value.


6. **Django Setup**

	This assumes you have a `Django project` already started.
	1. Pip downloads:

		```
		pip install boto django-storages-redux
		```
	2. Add `'storages',` to `INSTALLED_APPS` in your Django Settings (such as in `settings.py`)
	3. Run `python manage.py migrate` to ensure `django-storages-redux` is installed. Django Storage Redux ([docs](https://pypi.python.org/pypi/django-storages-redux)) is a updated version of Django Storage ([docs](https://django-storages.readthedocs.org/en/latest/)) and should be considered as a viable replacement. 
	5. In your Django configuration folder where `settings.py` and `urls.py` are, create a new file called `utils.py`
	6. In `utils.py` add the following:

		```
		from storages.backends.s3boto import S3BotoStorage

		StaticRootS3BotoStorage = lambda: S3BotoStorage(location='static')
		MediaRootS3BotoStorage  = lambda: S3BotoStorage(location='media')
		```

	7. In your `settings.py` add the following:

		```
		AWS_ACCESS_KEY_ID = "<your_access_key_id>"
		AWS_SECRET_ACCESS_KEY = "<your_secret_access_key>"


		AWS_FILE_EXPIRE = 200
		AWS_PRELOAD_METADATA = True
		AWS_QUERYSTRING_AUTH = True

		DEFAULT_FILE_STORAGE = '<your-project>.utils.MediaRootS3BotoStorage'
		STATICFILES_STORAGE = '<your-project>.utils.StaticRootS3BotoStorage'
		AWS_STORAGE_BUCKET_NAME = '<your_bucket_name>'
		S3DIRECT_REGION = 'us-west-2'
		S3_URL = '//%s.s3.amazonaws.com/' % AWS_STORAGE_BUCKET_NAME
		MEDIA_URL = '//%s.s3.amazonaws.com/media/' % AWS_STORAGE_BUCKET_NAME
		MEDIA_ROOT = MEDIA_URL
		STATIC_URL = S3_URL + 'static/'
		ADMIN_MEDIA_PREFIX = STATIC_URL + 'admin/'

		import datetime

		two_months = datetime.timedelta(days=61)
		date_two_months_later = datetime.date.today() + two_months
		expires = date_two_months_later.strftime("%A, %d %B %Y 20:00:00 GMT")

		AWS_HEADERS = { 
			'Expires': expires,
			'Cache-Control': 'max-age=%d' % (int(two_months.total_seconds()), ),
		}
		```

	8. Run `python manage.py collectstatic` and you should be all setup.



Subscribe on our [YouTube Channel](http://joincfe.com/youtube) and join us for more in-depth tutorials on [Django development](http://joincfe.com/enroll).


Cheers!


#### Organized by CodingForEntrepreneurs
