# insure-me
Jenkin-server setup with installing Jenkins and Ansible

Make hosts file in /etc/ansible path for deployment with Ansible.

![image](https://github.com/harshpgoti/insure-me/assets/75650522/89b81ace-a562-4c9c-adfe-ad9a444a7b2f)

All three instances:
1)	Jenkins-server:
 
![image](https://github.com/harshpgoti/insure-me/assets/75650522/7aab5d6c-ba9e-4a13-8ad7-2c74947fc3da)

2)	Test server:

![image](https://github.com/harshpgoti/insure-me/assets/75650522/30aa412f-6930-4c7e-9dcb-4bb20532f001)

3)	Prod-server:

![image](https://github.com/harshpgoti/insure-me/assets/75650522/aa946072-9181-45ba-9423-f81243c43619)


Two git repo:

https://github.com/harshpgoti/insure-me

https://github.com/harshpgoti/insure-me-selenium-script


Three jenkins pipelines:
1) capstone-insure-me-prod-server
2) capstone-test-server
3) capstone-docker-build-push

![image](https://github.com/harshpgoti/insure-me/assets/75650522/fb5753ce-6186-43c1-a9e8-b40c50338258)



# Explanation:

1) capstone-insure-me-prod-server: checked out, compiled, tested, packaged and containerized in test-server
Pipeline script:

![image](https://github.com/harshpgoti/insure-me/assets/75650522/51fda467-5029-4940-9ca8-0dbe04205eec)

With this script, the pipeline will clone the repo, build the docker image using Dockerfile, and push it to the docker hub for deployment.
 
Pipeline output:

![image](https://github.com/harshpgoti/insure-me/assets/75650522/d1cb2607-a78f-470e-9f83-d8db319b4e11)

![image](https://github.com/harshpgoti/insure-me/assets/75650522/82d4d2e5-6b30-40b1-be0b-41c4586a82a7)

![image](https://github.com/harshpgoti/insure-me/assets/75650522/ed87269e-2efd-4ae4-9b54-b7ed39639a9d)



2) capstone-test-server: deployed to the preconfigured test-server, deployment will be tested using a test automation
This job will run if it first got success response.

![image](https://github.com/harshpgoti/insure-me/assets/75650522/0ff6dfc7-cab5-4947-9f47-85a96bf51819)

Pipeline script:

![image](https://github.com/harshpgoti/insure-me/assets/75650522/9f9e2132-cb98-4e22-b32d-045da05b84a8)

With this script, the pipeline will clone the “insure-me” repo and run the following ansible file from the repo in the test server. With that, it will pull the docker image from the docker hub repo and run it for test deployment.

![image](https://github.com/harshpgoti/insure-me/assets/75650522/b7dec1fb-94f5-424a-abbe-cdae48d22a35)

After it, the pipeline will clone the “insure-me-selenium-script” repo and run the following ansible file from the repo. With that, it will run a .jar file of the automation selenium script and capture images.

![image](https://github.com/harshpgoti/insure-me/assets/75650522/5f2ae8db-17c9-4e5f-8a15-1a594d02d71d)

 
Pipeline output:

![image](https://github.com/harshpgoti/insure-me/assets/75650522/c3306ea9-d061-43a8-a2dc-2d65b6d875eb)
 
![image](https://github.com/harshpgoti/insure-me/assets/75650522/ca4c6d87-af2a-4333-8954-d3ba332cc715)

![image](https://github.com/harshpgoti/insure-me/assets/75650522/d99b6fff-5429-4a67-9145-c6a2b2f08321)

![image](https://github.com/harshpgoti/insure-me/assets/75650522/1e2e5c1b-09af-4734-a1fe-185bf3beaa19)





3) capstone-docker-build-push: if the build is successful, it should be deployed to the prod server
This job will run if the second got success response.

![image](https://github.com/harshpgoti/insure-me/assets/75650522/de958dc6-47e1-4beb-98b6-0135dc975683)

Pipeline script:

 ![image](https://github.com/harshpgoti/insure-me/assets/75650522/a69c630b-f92f-49f0-8435-c57dfc7be2c6)

With this script, the pipeline will clone the “insure-me” repo and run the following ansible file from the repo in Prod-server. With that, it will pull the docker image from the docker hub repo and run it for production deployment.

 ![image](https://github.com/harshpgoti/insure-me/assets/75650522/5ad8245c-28b2-48b2-8850-d5c4b1729550)

Pipeline output:

![image](https://github.com/harshpgoti/insure-me/assets/75650522/26ba5021-0b13-4efd-a5e2-7c1f558d4d89)

![image](https://github.com/harshpgoti/insure-me/assets/75650522/fd74098b-8e80-4982-9736-88045d5b4bd4)

![image](https://github.com/harshpgoti/insure-me/assets/75650522/ce8451d1-3f3a-446e-b4f5-289ba9e1a8f9)

![image](https://github.com/harshpgoti/insure-me/assets/75650522/805926d9-ba83-4a03-94ad-94f2b5aca929)