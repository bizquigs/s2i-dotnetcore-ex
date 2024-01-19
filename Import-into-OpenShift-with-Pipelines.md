# Let’s import a .NET 8 application from a GitHub repo into our OpenShift cluster

(and run a basic CI/CD Pipeline)


## Prerequisites:

We need to make sure our OpenShift version has the appropriate .NET 8 image. If not, we’ll add it.
<br>
<br>
First, let’s see if there are any .NET images.
```
oc get imagestream dotnet -o yaml -n openshift |grep description
```
![Screenshot 2023-12-15 at 4 56 23 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/a0e2ce5e-92f3-4789-8580-015d5aad1832)

Look at the dotnet ones. There is no .NET 8, which we want.
<br>
<br>
Let’s add .NET 8 images.

```
oc apply -f https://raw.githubusercontent.com/redhat-developer/s2i-dotnetcore/main/dotnet_imagestreams.json -n openshift
```

<br>
You can ignore any warnings about   

```kubectl.kubernetes.io/last-applied-configuration```  

![Screenshot 2024-01-17 at 2 41 25 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/1a44e758-fd65-4773-b448-0b80b893266d)

Now we have .NET 8  

You can verify with this:
```
oc get imagestream dotnet -o yaml -n openshift |grep description
```

![Screenshot 2023-12-15 at 4 59 54 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/edbbe4c7-c075-4f84-9e12-6c6f1463ea26)

<br>
<br>

### Make sure we have the OpenShift Pipelines Operator installed  

First click on Operators -> Installed Operators to see if it's already installed. If not, the do the following:  
<br>
![Screenshot 2024-01-17 at 3 01 54 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/10fbb1a7-0240-4a3b-a19d-42d2a55c73d0)

![Screenshot 2024-01-17 at 3 06 14 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/99856d6e-88b9-47d1-aad9-24dd90816c7e)

![Screenshot 2024-01-17 at 3 07 30 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/2d0a27e4-09b8-419b-b5d5-3ed8964b9a95)  


## Switch to Developer view and create a project

![Screenshot 2024-01-17 at 3 12 37 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/664447aa-20e0-4aba-8402-33c2c010b411)

![Screenshot 2024-01-17 at 2 43 00 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/fcf15b75-ff1b-467a-a06f-30b15903ef21)

## Deploy the .NET app

Select Import from Git

![Screenshot 2024-01-17 at 2 45 59 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/4a19f4bd-9b1f-4ebf-a727-52e4dbea3fc0)  

<br>

Copy this .NET sample app repo URL:
```
https://github.com/redhat-developer/s2i-dotnetcore-ex
```

<br>

![Screenshot 2024-01-17 at 2 49 10 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/7af6aca3-79a7-462e-ada3-9e8ce2cce6b8)


![Screenshot 2024-01-17 at 2 51 52 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/b6bc9bb0-af67-4962-b28c-f29f600f22ae)

![Screenshot 2024-01-17 at 2 53 52 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/64b13952-6208-474c-adf8-9d1c297135a6)

![Screenshot 2024-01-17 at 2 55 39 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/5b42a6fe-c516-48f4-a939-ff5dde5e42c5)

![Screenshot 2024-01-17 at 3 17 06 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/17e6abe1-5ba1-4e4c-b262-c4ac689828fa)

![Screenshot 2024-01-17 at 3 18 44 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/7e38a490-4acb-4e23-8731-e385c4423a08)

Now we can see the application topology
![Screenshot 2024-01-17 at 3 20 54 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/96ebde28-e6de-41f0-93e3-70047382f467)

![Screenshot 2024-01-17 at 3 59 01 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/08e269a6-158d-4249-aaa1-12749cf3da24)

![Screenshot 2024-01-17 at 4 01 04 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/935f73fa-232c-47f6-8383-ff1b95a2eb07)

![Screenshot 2024-01-17 at 4 02 22 PM](https://github.com/bizquigs/s2i-dotnetcore-ex/assets/78877185/81e1b3bd-9381-46d0-a0fe-5e7518746efb)





