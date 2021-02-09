# Business Logic Errors

## **Introduction**
Business Logic Errors are ways of using the legitimate processing flow of an application in a way that results in a negative consequence to the organization.

## **How to Find**
1. Review Functionality
   - Some applications have an option where verified reviews are marked with some tick or it's mentioned. Try to see if you can post a review as a Verified Reviewer without purchasing that product.
   - Some app provides you with an option to provide a rating on a scale of 1 to 5, try to go beyond/below the scale-like provide 0 or 6 or -ve.
   - Try to see if the same user can post multiple ratings for a product. This is an interesting endpoint to check for Race Conditions.
   - Try to see if the file upload field is allowing any exts, it's often observed that the devs miss out on implementing protections on such endpoints. 
   - Try to post reviews like some other users.
   - Try performing CSRF on this functionality, often is not protected by tokens

2. Coupon Code Functionality 
   - Apply the same code more than once to see if the coupon code is reusable. 
   - If the coupon code is uniquely usable, try testing for Race Condition on this function by using the same code for two accounts at a parallel time.
   - Try Mass Assignment or HTTP Parameter Pollution to see if you can add multiple coupon codes while the application only accepts one code from the Client Side. 
   - Try performing attacks that are caused by missing input sanitization such as XSS, SQLi, etc. on this field
   - Try adding discount codes on the products which are not covered under discounted items by tampering with the request on the server-side. 

3. Delivery Charges Abuse 
   - Try tampering with the delivery charge rates to -ve values to see if the final amount can be reduced.
   - Try checking for the free delivery by tampering with the params.

4. Currency Arbitrage 
   - Pay in 1 currency say USD and try to get a refund in EUR. Due to the diff in conversion rates, it might be possible to gain more amount.
  
5. Premium Feature Abuse 
   - Try forcefully browsing the areas or some particular endpoints which come under premium accounts.
   - Pay for a premium feature and cancel your subscription. If you get a refund but the feature is still usable, it's a monetary impact issue.
   - Some applications use true-false request/response values to validate if a user is having access to premium features or not.
   - Try using Burp's Match & Replace to see if you can replace these values whenever you browse the app & access the premium features.
   - Always check cookies or local storage to see if any variable is checking if the user should have access to premium features or not.

6. Refund Feature Abuse
   - Purchase a product (usually some subscription) and ask for a refund to see if the feature is still accessible.
   - Try for currency arbitrage explained yesterday.
   - Try making multiple requests for subscription cancellation (race conditions) to see if you can get multiple refunds.

7. Cart/Wishlist Abuse 
   - Add a product in negative quantity with other products in positive quantity to balance the amount.
   - Add a product in more than the available quantity.
   - Try to see when you add a product to your wishlist and move it to a cart if it is possible to move it to some other user's cart or delete it from there.

8. Thread Comment Functionality
   - Unlimited Comments on a thread
   - Suppose a user can comment only once, try race conditions here to see if multiple comments are possible.
   - Suppose there is an option: comment by the verified user (or some privileged user) try to tamper with various parameters in order to see if you can do this activity.
   - Try posting comments impersonating some other users.

9. Parameter Tampering 
   - Tamper Payment or Critical Fields to manipulate their values
   - Add multiple fields or unexpected fields by abusing HTTP Parameter Pollution & Mass Assignment
   - Response Manipulation to bypass certain restrictions such as 2FA Bypass 

Reference:
- [@harshbothra_](https://twitter.com/harshbothra_)