---
title: "Utilizing Mock Servers for API Testing"
seoTitle: "Mock Servers: API Testing Optimization"
seoDescription: "Optimize API testing using Postman mock servers for early automated test case creation, validation, and enhanced Agile development efficiency"
datePublished: Sun Aug 20 2023 23:43:14 GMT+0000 (Coordinated Universal Time)
cuid: cllk3g83h000008mk9bt9fnpx
slug: utilizing-mock-servers-for-api-testing
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692572425025/333924e1-70de-45e7-b768-475df45440dc.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692574775685/504f8e4d-46d9-4d3f-950e-03ab831e4e97.jpeg
tags: postman, mock-api-server, postman-mock-sever

---

## Why Mock Servers

You may have noticed a small server icon on the sidebar of Postman and wondered about its purpose. Today, we will explore its function together.

As the term "mock" suggests, it is intended to simulate the real behavior of an object or system. In Postman, this refers to imitating the behavior of APIs before they are developed, assuming we know their intended functionality and expected responses. This is beneficial for testing in two primary ways.

Firstly, it allows us to begin writing automated test cases while developers are still in the process of creating the APIs, and before they are available for testing in specific environments. This is particularly useful in the Agile development model, as testers do not have to wait until APIs are fully developed.

Secondly, it enables us to test the cases for invalid scenarios when an API would return 4XX or 5XX responses, among others. For example, consider an API for which we want to write test cases when it fails to connect to a database. We can write the test case, but we cannot test the logic unless the API fails to connect to the database. Instead of waiting for this to happen, we can utilize a mock server that returns the same response code and response body as the actual API would when it fails, allowing us to test our code logic. To better understand this concept, let us examine each use case in more detail.

## We can accomplish our goal in four steps:

1. Create a mock server.
    
2. Set up mock requests and corresponding responses according to API rules.
    
3. Write test cases in Postman that will run with each execution.
    
4. Execute the request with changes in payload and verify test results.
    

## Create a Mock Server.

The Postman documentation provides a comprehensive guide for [setting up mock servers](https://learning.postman.com/docs/designing-and-developing-your-api/mocking-data/setting-up-mock/). Additionally, you can refer to my [article on setting up mock servers](https://tajindersinghdhoot.hashnode.dev/mastering-mock-servers-in-postman-a-step-by-step-guide), which includes a practical example for a more in-depth understanding.

## Rules to Test Our Mock API.

We will create a mock example of an API that returns the shipping fee for a customer based on the total amount of cart items and the type of active subscriptions held by the customer. The rules are as follows:

1. Allow two shipping methods: 'standard' and 'prime'.
    
2. Charge no shipping fee for customers with active memberships, irrespective of shipping method and cart amount.
    
3. Charge a $6.99 shipping fee for 'standard' shipping method, cart amount less than $35, and inactive membership.
    
4. Charge a $13.99 shipping fee for 'prime' shipping method and inactive membership, regardless of cart amount.
    

### Valid Test Scenarios

Based on the rules specified above, there are certain test cases (TCs) that we can automate using Postman. Some of them are listed below:

1. Shipping method: 'standard', cart amount: &lt;$35, membership: active.
    
2. Shipping method: 'standard', cart amount: &lt;$35, membership: inactive.
    
3. Shipping method: 'standard', cart amount: &gt;=$35, membership: active.
    
4. Shipping method: 'standard', cart amount: &gt;=$35, membership: inactive.
    
5. Shipping method: 'prime', cart amount: &lt;$35, membership: active.
    
6. Shipping method: 'prime', cart amount: &lt;$35, membership: inactive.
    

Let's examine the first example. The left panel displays the expected request payload, while the right panel presents the anticipated response code and response body. If the chosen shipping method is standard shipping, the cart amount is less than $35, and the customer has an active membership, no shipping fee will be applied. Essentially, we are instructing the server to return the response on the right side when it receives the request payload on the left side.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692565239938/4f054381-a0cf-4159-8424-2fa6cf05be2b.png?auto=compress,format&format=webp align="left")

Examining the second scenario, the left side represents the anticipated request payload, while the right side illustrates the expected response code and response body. If the chosen shipping method is standard shipping, the cart amount is under $35, and the customer possesses an inactive membership, a shipping fee of $6.99 will be applied to the customer's order.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692567959953/8a49c8da-2430-4ce3-a317-d682d6aab842.png align="center")

Examining another example, this time involving Prime shipping: If the selected shipping method is 'Prime' shipping, regardless of the cart amount, and the customer has an inactive membership, a shipping fee of $13.99 will be applied to the customer's order. Similarly, more examples can be created based on the relevant test cases.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692568087659/d96b5f48-0e35-4c17-aaae-fe6c578ed654.png align="center")

We have completed the configuration of the mock response examples based on payloads. Now, let us proceed to call the mock API by making adjustments to the payload.

In the following illustration, we attempted to send a request payload with the selected shipping method as 'standard', a cart amount exceeding $35, and an active membership. We successfully obtained the expected response code and response body, with a shipping fee of $0 (Test Case 3 in the list of test cases mentioned previously in valid test scenarios list). The console displays the full URL with the endpoint path, as well as the request and response headers and body.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692568426120/a7536229-4795-421c-9eda-47ef5a929caa.png align="center")

Similarly, by modifying the payload, it is possible to evaluate whether the anticipated shipping fees are obtained for the remaining test cases.

### Invalid Test Scenarios

In addition to evaluating the functionality of APIs, it is imperative to assess invalid test scenarios, including those yielding 4XX and 5XX response codes. The following examples illustrate various test cases and demonstrate how to configure them within Postman:

* Invalid values for selected shipping.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692570958524/7e78f21c-9d47-43d9-91a5-d76902e80875.png align="center")

* Amount should not be negative.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692571019992/3d9cbc82-472c-4265-9eab-5fb6f458b2d3.png align="center")

* Content-Type should be json/application. Expected 415 if anything else.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692574176264/f01f49a3-29af-42c3-95c1-35cfe4d9ff7a.png align="center")

## Write Test Cases in Postman

We have successfully established the examples. Now, let us proceed to compose test cases that will be executed upon sending the request in the Postman. Test cases can be formulated within the "Test" tab of Postman. The tests are accessible at [https://github.com/Tajinder-Dhoot/postman-mock-server-tests/blob/main/test.js](https://github.com/Tajinder-Dhoot/postman-mock-server-tests/blob/main/test.js).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692571510579/1bdf8bb9-05a3-41d7-b7b6-fb9a307df9fd.png align="center")

## Send Request and Verify Test Results

Final Step: Establish Mock Server and Validate Test Cases

This marks the culmination of configuring the mock server and ascertaining the dependability of the test cases we have developed, which can be employed subsequently for evaluating the actual API. As demonstrated below, the test cases have successfully passed, contingent upon the payload transmitted alongside the request.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692571971775/538db05c-8572-4d7d-8555-0b669aec457e.png align="center")

The test cases can be explored with various payloads from our examples, making the process more efficient. Thankfully, we don't need to do this manually. In these situations, Postman's 'Runner' becomes our greatest ally. We'll delve into this further in an upcoming blog post.

I trust this blog has been valuable in guiding you through setting up the mock server and testing your APIs, particularly if you're new to Postman.

Looking forward to seeing you in our next blog post. In the meantime, stay connected, stay healthy, and keep learning. Thank you for stopping by, and cheers to your success!