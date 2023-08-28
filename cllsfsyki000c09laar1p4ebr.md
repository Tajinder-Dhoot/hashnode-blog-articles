---
title: "Setting up Mock Servers in Postman: A Step-by-Step Guide"
seoTitle: "Postman Mock Servers Setup: Step-by-Step Guide"
seoDescription: "Master Postman's Mock Servers with this step-by-step guide: create, configure, and test API responses for various scenarios to streamline development"
datePublished: Sat Aug 26 2023 19:51:13 GMT+0000 (Coordinated Universal Time)
cuid: cllsfsyki000c09laar1p4ebr
slug: setting-up-mock-servers-in-postman-a-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/FPK6K5OUFVA/upload/791978ba30159586cbd0aedb26479318.jpeg
tags: postman, mock-server, postman-mock-server

---

Click on the "Mock Servers" button in the left sidebar, then click the "Create Mock Server" button.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692563173007/515bcadc-ba86-4ca6-ac80-2c81c8777eaf.png align="center")

Fill in the 'Request URL' for the API you will be testing. The API architecture or development team can provide this information. You can change this later, so feel free to enter any value you believe is appropriate.

a. For now, let's assume that the response code returned will be 200 OK. This can be changed later.

b. The response body can be left empty, as we will add this later.

c. The request method will depend on the API being tested, but it can also be changed later. Click "Next." In this example, we will examine a mock API that returns a shipping fee based on the shipping method selected by the user and the cart amount. I have named this mock server "Shipping Fee," but you can name it according to your needs. The rest of the settings can be left as default for now.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692564387402/5a3f5011-1624-4e85-9362-2c2c0f8b4af8.png align="center")

You will see a mock server created with the specified specifications. The URL provided below is the URL that will be used to call this mock API. Later, this will be replaced by the actual API URL when it becomes available for testing in the testing environment.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692564627889/03eae426-d8ab-4d40-b4c2-6e783266abbf.png align="center")

Click on 'Collections' in the sidebar. A collection should have been automatically generated with the same name as the mock server. This collection will contain one mock example. Within this example, you can define the request payload, the corresponding response payload, and the response code. I have included additional examples for further exploration, but let's first examine the initial example. The left panel displays the expected request payload, while the right panel presents the anticipated response code and response body. If the chosen shipping method is standard shipping, the cart amount is less than $35, and the customer possesses an active membership, no shipping fee will be applied. In essence, we are instructing the server to return the response on the right side when it receives the request payload on the left side.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692565239938/4f054381-a0cf-4159-8424-2fa6cf05be2b.png align="center")

In the second example, the left side illustrates the incoming request payload and the right side displays the predicted response code and response body. When the selected shipping method is standard shipping, the cart total is below $35, and the customer holds an active membership, a shipping fee of $6.99 will be imposed on the customer.

If you submit the payload in this example, the response will indicate a shipping fee of $6.99. *<mark>It is essential to ensure that Postman automatically generates the response from a mock example based on the request payload.</mark>*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692567959953/8a49c8da-2430-4ce3-a317-d682d6aab842.png align="center")

Similarly, we can establish other examples according to our API guidelines. Great job! We have successfully set up the mock server. I hope this article proves helpful if you're facing difficulties.

See you soon in another blog post. Until then, stay connected, stay healthy, and keep learning. Thank you for visiting, and cheers!