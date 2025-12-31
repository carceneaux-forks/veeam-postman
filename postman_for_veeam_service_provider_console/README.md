# Postman for Veeam Service Provider Console (VSPC)

[Postman](https://www.getpostman.com/) is a tool that’s build by developers for developers. It provides a complete API development environment with stream-lined collaboration to help any number of use cases including testing, development, & product development. They do have both [free and paid versions](https://www.getpostman.com/pricing) so if you are looking at getting started, they make it easy and you can work your way up.

Importing VSPC REST API into Postman was originally mentioned in a [blog post](https://www.cragdoo.co.uk/2017/08/17/veeam-availability-console-api/) by Craig Dalrymple. The method mentioned here not only covers that but automates auth for **all** API calls.

## Requirements

* Veeam Service Provider Console
* [Postman](https://www.getpostman.com/)

## Getting Started

* Get the VSPC OpenAPI specification located in the [Veeam Help Center Documentation](https://helpcenter.veeam.com/references/vac/9.1/rest)

![Download OpenAPI specification](images/download_openapi_specification.png)

* Alternatively, you can find the specification on your local VSPC instance
  * To get this, you'll have to navigate to a URL hosted on your VSPC web server
  * Click the link shown below which triggers a file download:
    * `https://<vspc_web_server>:1280/api/swagger/index.html`

![VSPC OpenAPI specification](images/vspc_openapi_specification.png)

* Import the file we just downloaded into Postman

![Postman Import](images/postman_import.png)

* Make sure `OpenAPI 2.0 Specification with a Postman Collection` is selected

![OpenAPI 2.0 Specification with a Postman Collection](images/postman_import_generate.png)

* Click `Import`
  * **Wait...be patient!**

![Postman import status](images/postman_import_status.png)

* Once imported, it will show up in your Postman Collections as shown below:

![VSPC Postman Collection](images/vspc_postman_collection.png)

* Set the following [variables](https://learning.getpostman.com/docs/postman/environments_and_globals/variables/) in Postman:
  * `baseUrl`: Base URL of Veeam Service Provider Console web server
    * _This can be configured while editing collection in a step below._
  * `vspc-username`: Username login
  * `vspc-password`: Password login

* Open the newly imported collection and navigate to the `token` -> `OAuth 2.0 Authentication` API call
* Click on the `Params` tab
  * Uncheck all parameters

![Uncheck parameters](images/uncheck_params.png)

* Click on the `Authorization` tab
  * Set _Auth Type_ to `No Auth`

![No auth type](images/no_auth_type.png)

* Click on the `Body` tab
  * Update fields as shown below:

![VSPC Login Body](images/login_body.png)

* Click on the `Scripts` tab
* Copy/Paste the code from [here](automated_auth_test.js) in this section

![VSPC Login Tests](images/login_test.png)

* Click `Save` at the top-right
* Edit the collection settings by clicking on the root folder

![VSPC Collection Edit](images/vspc_collection_edit.png)

* Navigate to the `Authorization` tab
* Choose _Auth Type:_ `Bearer Token`
* Enter for _Token:_ `{{vspc_access_token}}`

![VSPC Collection Auth](images/vspc_collection_auth.png)

At this point, you've now automated auth for **all** API calls! All you have to do when using an API call in this collection is make sure that `Authorization` is set to _Type:_ `Inherit auth from parent`

![VSPC Auth Type](images/auth_type.png)

You can now begin using Postman with the Veeam Service Provider Console!
