---
template: templates/swagger.html
---

<<<<<<<< HEAD:en/identity-server/6.0.0/docs/apis/fido-rest-api.md
# FIDO 2 Rest API Definition

??? Note "Click For instructions"
    Follow the steps given below to try out the REST APIs with your local instance of WSO2 Identity Server.
========
# FIDO 2 Rest API Definition - v2

??? Note "Click For Instructions"
    Do the following to try out the REST APIs with your local instance of WSO2 Identity Server. 
>>>>>>>> 5.11.0-docs-old:en/identity-server/5.11.0/docs/develop/fido-rest-api.md
    
    1.  Click **Authorize** and provide the desired values for authentication. 
    2.  Expand the relevant API operation and click the **Try It Out** button.  
    3.  Fill in relevant sample values for the input parameters and click **Execute**. 
        You will receive a sample curl command with the sample values you filled in. 
    4. Add a `-k` header to the curl command and run the curl command on the terminal with a running instance of WSO2
     IS. 

<div id="swagger-ui"></div>
<script>

  // Begin Swagger UI call region
  const ui = SwaggerUIBundle({
<<<<<<<< HEAD:en/identity-server/6.0.0/docs/apis/fido-rest-api.md
     url: "{{base_path}}/apis/restapis/fido.yaml",
========
    url: "https://raw.githubusercontent.com/wso2-extensions/identity-local-auth-fido/v5.2.8/components/org.wso2.carbon.identity.application.authenticator.fido2.endpoint/src/main/resources/fido.yaml",
>>>>>>>> 5.11.0-docs-old:en/identity-server/5.11.0/docs/develop/fido-rest-api.md
    dom_id: '#swagger-ui',
    deepLinking: true,
    validatorUrl: null,
    presets: [
      SwaggerUIBundle.presets.apis,
      SwaggerUIStandalonePreset
    ],
    plugins: [
      SwaggerUIBundle.plugins.DownloadUrl
    ],
    layout: "StandaloneLayout"
  })
  // End Swagger UI call region

   window.ui = ui
</script>