# Netlify deployment of github private repo

If you want to deploy github **private repo** to netlify, using **netlify API**. Here is a step by step procedure.

1. Firstly you need to get the **id** of the github repo, which you want to deploy. know how to get the github id [here.](https://developer.github.com/v3/repos/#get-a-repository)
2. After getting repo **id**, You have to get **public_key** & **id** using **netlify api.** know how to get the **public_key** [here.](https://open-api.netlify.com/?_ga=2.63446895.1198490019.1605279725-1481263431.1601888080#operation/createDeployKey)
3. After getting **public_key**, Using github api `https://api.github.com/repos/:owner/:repo/keys` **POST** **public_key** in the body section as shown below

```
{
    "title":"test",
    "key":<your public key>,
    "read_only":false
}
```
4. After this step deploy the site using `https://api.netlify.com/api/v1/sites`. Use **POST** method by **body** as below

```
{
  "name":<your site name>, // ex: test
  "repo":{
      "provider":"github",
      "id":<your github repo id>,
      "repo":"<your username>/<your repo>",
      "private":true,
      "branch":"main",
      "deploy_key_id":<your deploy key id>
  }
}
```

In the above **deploy_key_id** is the **id** you got in the 2nd step.
5. Boom!! congratulations, your site has been deployed successfully.
