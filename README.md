## Prerequisites

- [.NET 8 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)  
- [Node.js](https://nodejs.org/en/download/) (v16 or higher recommended)  
- npm (included with Node.js)  
- Code editor such as VS Code  
- Internet access for package restoration  

## Project Structure

newmark-assessment/  
├── backend/  
│   └── Newmark.Api/          # C# backend API project  
└── frontend/  
    └── newmark-ui/           # React frontend project  

## Backend API Setup and Execution

1. Open a terminal or command prompt.  
2. Navigate to the backend directory:  
   cd newmark-assessment/backend/Newmark.Api  
3. Restore dependencies:  
   dotnet restore  
4. Run the backend API:  
   dotnet run  
5. The API will start and listen on configured URLs (e.g., https://localhost:7096).  
6. Confirm the API is accessible by navigating to:  
   https://localhost:7096/api/properties  

## Frontend React Application Setup and Execution

1. Open a separate terminal window.  
2. Navigate to the frontend directory:  
   cd newmark-assessment/frontend/newmark-ui  
3. Install Node.js dependencies:  
   npm install  
4. Start the development server:  
   npm start  
5. The React app will launch at http://localhost:3000 and communicate with the backend API.

## Configuration Details

- The backend API must be running before starting the frontend application to ensure successful API calls.  
- If backend ports or URLs are changed, update the API endpoint URL accordingly in the frontend code (commonly in App.js or environment variables).  
- Cross-Origin Resource Sharing (CORS) is enabled in the backend for localhost origins to allow requests from the frontend development server.  
- The Azure Blob Storage SAS token and URL must be valid and correctly configured in the backend to avoid authentication errors.

## Error Handling and Diagnostics

- The frontend displays error messages when API calls fail (e.g., "Failed to fetch properties"). Verify the backend is running and accessible if this occurs.  
- Backend returns appropriate HTTP status codes and error messages in case of invalid SAS tokens or inaccessible blobs.  
- For 403 errors related to blob storage, confirm the SAS token validity, permissions, and expiry dates.  
- Network or firewall settings may block requests; ensure required ports are open for localhost communication.

## Functional Overview

- Backend API retrieves JSON data from Azure Blob Storage using the provided SAS token.  
- The JSON data is deserialized into strongly-typed C# models (Property, Space, RentRoll, etc.).  
- API endpoint /api/properties serves the transformed data as JSON.  
- The React frontend fetches this data and renders it hierarchically:  
  - Properties with fields such as Features, Highlights, and Transportation.  
  - Nested Spaces under each Property.  
  - RentRoll data (e.g., rents per month) under each Space.  
- Collapsible UI sections allow for an improved user experience and better data navigation.  
- Both backend and frontend implement asynchronous operations and error handling for responsiveness and robustness.

## Troubleshooting and Best Practices

- If backend port conflicts arise, update the port configuration in launchSettings.json located in Newmark.Api/Properties/.  
- Always start the backend API before the frontend to avoid fetch errors.  
- Validate the SAS token regularly; refresh as needed to maintain access to Azure Blob Storage.  
- Use environment variables or secure configuration management for sensitive data such as SAS tokens in production scenarios.  
- Follow SOLID principles and clean architecture practices in code organization for maintainability.  
- Monitor network logs in browser developer tools to diagnose frontend API communication issues.

---

This document serves as a comprehensive guide to build, run, and troubleshoot the Newmark Technical assessment solution.
