---
title: "Leveraging Postman Runners for Efficient API Testing"
seoTitle: "Optimizing API Testing with Postman Runners"
seoDescription: "Optimize API testing using Postman Runners for automated scenarios, streamlining regression tests, saving time, and boosting efficiency"
datePublished: Sun Oct 15 2023 19:48:23 GMT+0000 (Coordinated Universal Time)
cuid: clnrvpwn9000009mlfwl597bt
slug: leveraging-postman-runners-for-efficient-api-testing
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/FPK6K5OUFVA/upload/15faf0a5e9fb34199a551c6186e5c507.jpeg
tags: postman, postmanapi, postman-runners

---

## Introduction

In Postman, the utilization of Runners significantly benefits software testers. These Runners can mainly be employed in two distinct methods within the platform.

1. To ensure the APIs are working as expected which can be linked together. e.g., Post request to add a record in DB -&gt; GET request to confirm it has been added -&gt; UPDATE/ DELETE request to update/ delete a record from DB -&gt; Confirm the record has been updated/ deleted. (This can also be attained by chaining calls together with "Send Request" in the "Test" script of Postman)
    
2. The second is to test multiple test scenarios with a single click. But we must have the TCs automated in Postman to achieve this task. Postman has a very comprehensive [guide](https://learning.postman.com/docs/writing-scripts/test-scripts/) on how to automate the TCs in Postman. *<mark>This blog post is about the second use of runners.</mark>*
    

In certain situations, you may encounter numerous scenarios for the request body of an API, each with a unique response for the corresponding request payload. How can you efficiently test the test cases automated in Postman in such instances? Manually running the request for each test scenario would be time-consuming and laborious. Additionally, how would you handle any changes in the API development process? This is where Runners become an invaluable tool, as they facilitate the regression testing of APIs.

To better comprehend the functionality and advantages of Runners, we will employ a Mock API created using mock servers in Postman. If you are unfamiliar with the utilization of Mock Servers in Postman, I recommend referring to the [Postman documentation](https://learning.postman.com/docs/designing-and-developing-your-api/mocking-data/setting-up-mock/) or my blog on [creating mock servers](https://tajindersinghdhoot.hashnode.dev/setting-up-mock-servers-in-postman-a-step-by-step-guide). The mock server will simulate the behavior of the actual API, which will be developed by the team's developers.

## Rules for the API Being Tested

To demonstrate the application of runners in API testing, we will examine an API that returns the shipping fee, taking into consideration factors such as membership status, cart items price, and delivery method.

1. If the order is a pick-up order, no shipping fee will be applied.
    
2. If the order is a shipping order, the shipping fee will be based on the following factors.
    
3. Active members won't be charged any shipping fees.
    
4. Inactive members would be charged a shipping fee if the order amount after discounts is less than $35. The shipping fee would be:
    
    a. $6.99 for Standard Shipping
    
    b. $13.99 for Prime Shipping
    

## Test Cases for the API

By the stipulated guidelines, the following test cases have been provided for your reference. While additional test cases may be devised, these examples should sufficiently demonstrate the functionality of Postman runners.

1. delivery method is "pick up"; amount &lt; $35; amount after discounts &lt; $35; membership is inactive (shipping fee = 0)
    
2. delivery method is "pick up"; amount = $35; amount after discounts &lt; $35; membership is inactive (shipping fee = 0)
    
3. delivery method is "pick up"; amount &gt; $35; amount after discounts = $35; membership is inactive (shipping fee = 0)
    
4. delivery method is "pick up"; amount &gt; $35; amount after discounts &gt; $35; membership is inactive (shipping fee = 0)
    
5. delivery method is "standard"; amount &lt; $35; amount after discounts &lt; $35; membership is inactive (shipping fee = 6.99)
    
6. delivery method is "standard"; amount = $35; amount after discounts &lt; $35; membership is inactive (shipping fee = 6.99)
    
7. delivery method is "standard"; amount &gt; $35; amount after discounts = $35; membership is inactive (shipping fee = 0)
    
8. delivery method is "standard"; amount &gt; $35; amount after discounts &gt; $35; membership is inactive (shipping fee = 0)
    
9. delivery method is "express"; amount &lt; $35; amount after discounts &lt; $35; membership is inactive (shipping fee = 13.99)
    
10. delivery method is "express"; amount = $35; amount after discounts &lt; $35; membership is inactive (shipping fee = 13.99)
    
11. delivery method is "express"; amount &gt; $35; amount after discounts = $35; membership is inactive (shipping fee = 0)
    
12. delivery method is "express"; amount &gt; $35; amount after discounts &gt; $35; membership is inactive (shipping fee = 0)
    
13. delivery method is "pick up"; amount &lt; $35; amount after discounts &lt; $35; membership is active (shipping fee = 0)
    
14. delivery method is "pick up"; amount = $35; amount after discounts &lt; $35; membership is active (shipping fee = 0)
    
15. delivery method is "pick up"; amount &gt; $35; amount after discounts = $35; membership is active (shipping fee = 0)
    
16. delivery method is "pick up"; amount &gt; $35; amount after discounts &gt; $35; membership is active (shipping fee = 0)
    
17. delivery method is "standard"; amount &lt; $35; amount after discounts &lt; $35; membership is active (shipping fee = 0)
    
18. delivery method is "standard"; amount = $35; amount after discounts &lt; $35; membership is active (shipping fee = 0)
    
19. delivery method is "standard"; amount &gt; $35; amount after discounts = $35; membership is active (shipping fee = 0)
    
20. delivery method is "standard"; amount &gt; $35; amount after discounts &gt; $35; membership is active (shipping fee = 0)
    
21. delivery method is "express"; amount &lt; $35; amount after discounts &lt; $35; membership is active (shipping fee = 0)
    
22. delivery method is "express"; amount = $35; amount after discounts &lt; $35; membership is active (shipping fee = 0)
    
23. delivery method is "express"; amount &gt; $35; amount after discounts = $35; membership is active (shipping fee = 0)
    
24. delivery method is "express"; amount &gt; $35; amount after discounts &gt; $35; membership is active (shipping fee = 0)
    

## Illustration of a Few Test Cases

Allow me to provide a clear representation of the anticipated API request and response through specific examples.

The following image demonstrates a typical API request and its corresponding response in a scenario where the membership status is inactive, the shipping method selected is pick up, and the order amount post-discount is less than $35.

![Standard Shipping for inactive members when amount after discounts is less than 35](https://cdn.hashnode.com/res/hashnode/image/upload/v1697303153567/f8e3f1e0-83b4-4feb-8f09-e422350564b1.png align="center")

In the subsequent illustration, a representative example of an anticipated API request and response is depicted, wherein the membership status is inactive, the chosen shipping method is standard shipping, and the order total after discounts amounts to less than $35.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697303339718/bdbdcc84-8250-43a1-b9a8-b47700bd72d4.png align="center")

In the following illustration, another typical example of a projected API request and response is demonstrated, where the membership status is active, the selected shipping method is prime shipping, and the order total post-discount exceeds $35.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697303427910/c288bef0-d5a8-441b-8499-8cca736d6392.png align="center")

All the payloads for the test cases written above can be accessed from the [Git repository](https://github.com/Tajinder-Dhoot/shipping-fee-runner/blob/main/shipping_fee_payloads.json).

## Configure Runner Request

Upon successfully configuring the mock requests and responses, the subsequent step involves setting the body to retrieve the payload from the JSON file.

* Create separate request
    
* Set variable for body data in pre-request
    
* Use the variable in the request body as demonstrated below
    

```javascript
pm.collectionVariables.set("request_payload", JSON.stringify(pm.iterationData.toObject()));
```

The body of the runner request would look like this:

![Pre Request and Body Settings](https://cdn.hashnode.com/res/hashnode/image/upload/v1697386398894/dfd386bc-932b-4605-a01f-a1ac763536f3.png align="center")

## Writing the Test Script

Upon completing the configuration of payloads, establishing the body, and implementing the pre-request script, we shall proceed to develop the test script. Each test case within the script will execute for every request payload when utilizing the runner. The subsequent image illustrates the test script, which can be accessed from the [Git repo](https://github.com/Tajinder-Dhoot/shipping-fee-runner/blob/main/test_script.js). Feel free to incorporate additional test cases according to your requirements.

![Test Script](https://cdn.hashnode.com/res/hashnode/image/upload/v1697385893548/9eec0da9-aa71-40f9-923c-ed02b8e09c41.png align="center")

## Setting Up Runner

With the prerequisites in place for executing the test cases, we can now proceed to configure the runner with a JSON file. To do so, please adhere to the following steps:

* Click on the runner button in the bottom right of Postman. A window will open similar to the one displayed below.
    
* Drag and select the runner request in the 'Run order' area.
    
* Choose the JSON file containing all payloads. The file must have an array of all payloads. Each element in the array is considered a payload.
    

![Runner Settings](https://cdn.hashnode.com/res/hashnode/image/upload/v1697386796860/39babc21-3d25-4f63-be8a-b9a7bce4275c.png align="center")

## Executing Runner

Upon initiating the runner, all test cases will be executed for each payload within the file. Subsequently, the request, headers, and responses can be observed for each run execution.

![Runner Results](https://cdn.hashnode.com/res/hashnode/image/upload/v1697386987598/f9c38c6e-e202-434c-b1ad-7b95658b240a.png align="center")

## Summarizing

In the article, we discussed the use of Runners in Postman for automating and streamlining the testing of multiple API scenarios with a single click. Runners are essential for regression testing of APIs and help save time by avoiding manual testing for each test scenario. The article also mentions the use of a Mock API created using mock servers in Postman to demonstrate the working and benefits of Runners.

It is my sincere aspiration that the insights provided within this article will contribute to enhancing your proficiency in API testing. I look forward to engaging with you in future articles. In the meantime, maintain your well-being, stay connected, and continue your pursuit of knowledge.