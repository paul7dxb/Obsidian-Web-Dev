
# (Optional) Create New email account

- May be overprotective but its nice to have a separate account to what you use on other logins (in case of data breaches) 
	- Even if password is different may open you up to phishing attacks
	- Attackers now know of another email to try



# Sign Up

- [Sign Up](https://portal.aws.amazon.com/billing/signup?nc2=h_ct&src=header_signup&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start/email)

- Verify email
- Create very STRONG 💪 root password
	- We won't be using it to login and use the web GUI anyway if we create a seperate account to use
- $1 payment (does get refunded) 
- Verification stuff
- Basic support (free)
- Done!




# Login

- Sign in using root user
![[Pasted image 20231016211550.png|300]]

- This is the management console
	- There's lots here that will learn over time. Don't feel overwhelmed, just ignore most of it for now

# MFA (Essential)

- Go to dashboard
	- ![[Pasted image 20231016213905.png]]
- I use Google Authenticator but you can use 
	- ![[Pasted image 20231016214204.png|400]]
- Set up as required




# Create Account to Use (Recommended)

- Recommended not to use your root account
	- Especially is using access keys in future

- Use the search bar at the top to go to IAM (Identity Access Management)
![[Pasted image 20231016211902.png|600]]

- Click "users" on the left hand side nav bar
![[Pasted image 20231016211840.png|250]]

- Create User (yellow button)
- Provide user access to management console (tick)
	- Create IAM user
	- Custom password
	- Untick change password (its you)
![[Pasted image 20231016212753.png]]

- Add user to group
	- Create group
		- ![[Pasted image 20231016212936.png|600]]
	- Create user group
	- Assign group
		- ![[Pasted image 20231016213023.png]] 
		-  Next
	- Create User (yellow button)
- User is created
	- ![[Pasted image 20231016213146.png|400]]

## Login with account

- You need the account number or alias
	- Go to AWS dashboard (left hand navbar)
	- ![[Pasted image 20231016213335.png|400]]
	- You can create an alias to make it easier to login if you wish
		- Make note of whichever you want to use
	- Use the url in a private browser or incognito tab to make sure its working
		- ![[Pasted image 20231016213627.png|300]]
	- You will see you user info in top right
		- ![[Pasted image 20231016213659.png]]
	- 

## Harden Account

- This account has root permissions
	- Reduce permissions for this account for more security to just what you need
- Add MFA (as before)
- [Get an email whenever root is logged in](https://aws.amazon.com/blogs/mt/monitor-and-notify-on-aws-account-root-user-activity/)
- 




# Billing / Budget Alerts

## First step if user account set up
- Login as root
- Click account (top right) -> account
- Scroll down to IAM user and role access to billing information
	- Gives admins access to billing info
- ![[Pasted image 20231016215401.png]]

## Zero spend budget

- Set up a any cost billing alert
	- May require automatic forwarding if you set up a different email address before

- Click account (top right) -> my billing dashboard
	- ![[Pasted image 20231016215052.png|300]]
- Budgets (left hand side)
	- Create a budget
	- Use a template
	- Zero spend budget
	- Add email

- Similar for other budgets that notify at 85%, estimated 100% usage


# Debugging Costs

- Billing dashboard
- Bills
- Charges by service
- See what service is costing you
	- Also note regions