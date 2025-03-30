# Azure First-Time Setup Guide

This guide will walk you through creating an Azure account and establishing the minimal setup needed for your cloud environment.

## Step 1: Create an Azure Account

1. Go to [https://azure.microsoft.com/en-us/free/](https://azure.microsoft.com/en-us/free/)
2. Click the "Start free" button
3. Sign in with an existing Microsoft account or create a new one
4. Complete the registration process:
   - Provide your identity information
   - Verify your identity via phone or text
   - Enter your credit card details (required for verification)
   - Accept the subscription agreement

## Step 2: Set Up Billing Account and Subscription

### Billing Account Setup
1. During account creation, you'll be prompted to set up a billing account
2. Provide your billing information:
   - Legal company name (if applicable)
   - Billing address
   - Contact phone number
   - Email address for billing notifications

### Credit Card Information
1. Enter valid credit card details
   - This is required even for the free tier
   - The card will be charged once you exceed free tier limits or when the free tier expires
   - A temporary authorization charge may appear to verify your card (typically $1)
   - Ensure the card won't expire in the next few months

### Subscription Creation
Your first subscription will be created automatically during account setup (likely a free trial subscription). If you need a different subscription type:

1. Sign in to the [Azure Portal](https://portal.azure.com)
2. Search for "Subscriptions" in the search bar
3. Click "Add" to create a new subscription if needed
4. Select the appropriate offer (Pay-As-You-Go is common for production use)

## Step 3: Configure Microsoft Entra ID

Microsoft Entra ID (formerly Azure Active Directory) is your organization's identity foundation. It's automatically created when you set up your Azure account, but needs proper configuration:

1. Access Entra ID:
   - In the Azure Portal, search for "Microsoft Entra ID" or "Azure Active Directory"
   - Click on it to access your tenant

2. Configure company branding:
   - Select "Company branding" from the left menu
   - Upload your company logo, background images, and customize the sign-in experience
   - Click "Save"

3. Configure custom domain (recommended):
   - Select "Custom domain names" from the left menu
   - Click "Add custom domain"
   - Enter your organization's domain (e.g., yourcompany.com)
   - Click "Add domain"
   - Follow the verification process (requires adding DNS records)

4. Configure security defaults:
   - Select "Properties" from the left menu
   - Scroll down to "Security defaults" or access from Security > Properties
   - Enable security defaults for basic protection or disable if you plan to configure custom Conditional Access policies

5. Configure password policies:
   - Navigate to "Security" > "Authentication methods" > "Password protection"
   - Configure password expiration, complexity requirements, and banned passwords list
   - Click "Save"

## Step 4: Set Up User Groups and Permissions

Creating dedicated user groups with appropriate permissions will help maintain security and access control.

### Create Groups

1. In the Azure Portal, search for "Microsoft Entra ID" (formerly Azure Active Directory)
2. Select "Groups" from the left menu
3. Click "New group"
4. Create a DevOps group:
   - Group type: Security
   - Group name: "DevOps"
   - Group description: "Team members responsible for infrastructure and operations"
   - Click "Create"
5. Create a Developer group:
   - Group type: Security
   - Group name: "Developers"
   - Group description: "Team members responsible for application development"
   - Click "Create"

### Assign Permissions

1. Navigate to your subscription:
   - Search for "Subscriptions" in the portal
   - Select your subscription
   - Click on "Access control (IAM)" in the left menu

2. For DevOps team:
   - Click "Add" and select "Add role assignment"
   - Role: "Contributor" (can create and manage all resources but can't grant access to others)
   - Members: Select the "DevOps" group
   - Click "Review + assign"

3. For Developer team:
   - Click "Add" and select "Add role assignment"
   - Role: "Reader" (can view resources but not make changes)
   - Members: Select the "Developers" group
   - Click "Review + assign"
   
   - Optional: For specific resources developers need to modify:
     - Navigate to that specific resource
     - Go to "Access control (IAM)"
     - Add the Developers group with "Contributor" role just for that resource

### Invite Users

1. Return to Microsoft Entra ID
2. Select "Users" from the left menu
3. Click "New user" > "Invite external user"
4. Enter the user's email address
5. Add a personalized message (optional)
6. Click "Invite"
7. Once invited, add users to the appropriate group:
   - Go to the "Groups" section
   - Select either "DevOps" or "Developers" group
   - Click "Members" in the left menu
   - Click "Add members"
   - Search for and select the users you invited
   - Click "Select"

Each invited user will receive an email with a link to accept the invitation and join your Azure tenant.

## Billing Recommendations

1. Set up budget alerts:
   - In the Azure Portal, search for "Cost Management + Billing"
   - Select "Budgets" and create a new budget
   - Set reasonable spending limits and notification thresholds (e.g., 50%, 75%, 90%)
   - Add email recipients for alerts

2. Review your Azure pricing plan:
   - The free tier includes limited resources for 12 months
   - After that, you'll be on a pay-as-you-go model unless specified otherwise
   - Consider reservations for consistent workloads to reduce costs
