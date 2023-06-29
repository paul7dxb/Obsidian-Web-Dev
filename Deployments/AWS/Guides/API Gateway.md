# Enable CORS from site

To restrict CORS to a specific website (e.g., `https://example.com`), follow these steps:

1. Go to the AWS Management Console and open the API Gateway service.
2. Find and select your API.
3. In the left sidebar, click on "Resources."
4. Select the appropriate resource (e.g., the one you're using for the GET request).
5. In the "Actions" dropdown menu, select "Enable CORS."
6. A dialog box will appear. Click on "Enable CORS and replace existing CORS headers."
7. In the "Access-Control-Allow-Origin" field, enter the specific website origin (`https://example.com`).
8. Save the changes by clicking the "Save" button.