## ACCESS CONTROL (RBAC) :

- Role-based access control (RBAC) restricts network access based on a person's role within an organization and has become one of the main methods for advanced access control. The roles in RBAC refer to the levels of access that employees have to the network.

- Employees are only allowed to access the information necessary to effectively perform their job duties. Access can be based on several factors, such as authority, responsibility, and job competency. In addition, access to computer resources can be limited to specific tasks such as the ability to view, create, or modify a file.

- As a result, lower-level employees usually do not have access to sensitive data if they do not need it to fulfill their responsibilities. This is especially helpful if you have many employees and use third-parties and contractors that make it difficult to closely monitor network access. Using RBAC will help in securing your company’s sensitive data and important applications.
___
## EXAMPLES OF ROLE-BASED ACCESS CONTROL:  

-Through RBAC, you can control what end-users can do at both broad and granular levels. You can designate whether the user is an administrator, a specialist user, or an end-user, and align roles and access permissions with your employees’ positions in the organization. Permissions are allocated only with enough access as needed for employees to do their jobs.

- What if an end-user's job changes? You may need to manually assign their role to another user, or you can also assign roles to a role group or use a role assignment policy to add or remove members of a role group.

#### Some of the designations in an RBAC tool can include:

- Management role scope – it limits what objects the role group is allowed to manage.
- Management role group – you can add and remove members.
- Management role – these are the types of tasks that can be performed by a specific role group.
- Management role assignment – this links a role to a role group.

- By adding a user to a role group, the user has access to all the roles in that group. If they are removed, access becomes restricted. Users may also be assigned to multiple groups in the event they need temporary access to certain data or programs and then removed once the project is complete.

#### Other options for user access may include:

- Primary – the primary contact for a specific account or role.
- Billing – access for one end-user to the billing account.
- Technical – assigned to users that perform technical tasks.
- Administrative – access for users that perform administrative tasks.
___
## BENEFITS OF RBAC
Managing and auditing network access is essential to information security. Access can and should be granted on a need-to-know basis. With hundreds or thousands of employees, security is more easily maintained by limiting unnecessary access to sensitive information based on each user’s established role within the organization. Other advantages include:

1- Reducing administrative work and IT support. With RBAC, you can reduce the need for paperwork and password changes when an employee is hired or changes their role. Instead, you can use RBAC to add and switch roles quickly and implement them globally across operating systems, platforms and applications. It also reduces the potential for error when assigning user permissions. This reduction in time spent on administrative tasks is just one of several economic benefits of RBAC. RBAC also helps to more easily integrate third-party users into your network by giving them pre-defined roles.

2- Maximizing operational efficiency. RBAC offers a streamlined approach that is logical in definition. Instead of trying to administer lower-level access control, all the roles can be aligned with the organizational structure of the business and users can do their jobs more efficiently and autonomously.

3- Improving compliance. All organizations are subject to federal, state and local regulations. With an RBAC system in place, companies can more easily meet statutory and regulatory requirements for privacy and confidentiality as IT departments and executives have the ability to manage how data is being accessed and used. This is especially significant for health care and financial institutions, which manage lots of sensitive data such as PHI and PCI data.
____
## BEST PRACTICES FOR IMPLEMENTING RBAC

Implementing a RBAC into your organization shouldn’t happen without a great deal of consideration. There are a series of broad steps to bring the team onboard without causing unnecessary confusion and possible workplace irritations. Here are a few things to map out first.

-  Current Status: Create a list of every software, hardware and app that has some sort of security. For most of these things, it will be a password. However, you may also want to list server rooms that are under lock and key. Physical security can be a vital part of data protection. Also, list the status of who has access to all of these programs and areas. This will give you a snapshot of your current data scenario.

- Current Roles: Even if you do not have a formal roster and list of roles, determining what each individual team member does may only take a little discussion. Try to organize the team in such a way that it doesn’t stifle creativity and the current culture (if enjoyed).

- Write a Policy: Any changes made need to be written for all current and future employees to see. Even with the use of a RBAC tool, a document clearly articulating your new system will help avoid potential issues.

- Make Changes: Once the current security status and roles are understood (not to mention a policy is written), it’s time to make the changes.

- Continually Adapt: It’s likely that the first iteration of RBAC will require some tweaking. Early on, you should evaluate your roles and security status frequently. Assess first, how well the creative/production process is working and secondly, how secure your process happens to be.
___
# React-cookie :
### Minimum requirement

#### react-cookie @ v3.0+
- React.js >= 16.3.0 (new context API + forward ref)

#### react-cookie @ v0.0-v2.2
- React.js >= 15

## Getting started
- npm install react-cookie
or in the browser (global variable ReactCookie):
```js
<script
  crossorigin
  src="https://unpkg.com/react@16/umd/react.production.js"
></script>
<script
  crossorigin
  src="https://unpkg.com/universal-cookie@3/umd/universalCookie.min.js"
></script>
<script
  crossorigin
  src="https://unpkg.com/react-cookie@3/umd/reactCookie.min.js"
></script>

```


## '<CookiesProvider' />'
 
 Set the user cookies

On the server, the cookies props must be set using req.universalCookies or new Cookie(cookieHeader)

## useCookies([dependencies])

Access and modify cookies using React hooks.
```js
const [cookies, setCookie, removeCookie] = useCookies(['cookie-name']);
```
- React hooks are available starting from React 16.8

## cookies

Javascript object with all your cookies. The key is the cookie name.

## setCookie(name, value, [options])

Set a cookie value

- name (string): cookie name

- value (string|object): save the value and stringify the object if needed
- options (object): Support all the cookie options from RFC 6265

   - path (string): cookie path, use / as the path if you want your cookie to be accessible on all pages
  
   - expires (Date): absolute expiration date for the cookie
   
   - maxAge (number): relative max age of the cookie from when the client receives it in seconds
   
   - domain (string): domain for the cookie (sub.domain.com or .allsubdomains.com)
   
   - secure (boolean): Is only accessible through HTTPS? 
 
   - httpOnly (boolean): Can only the server access the cookie? Note: You cannot get or set httpOnly cookies from the browser, only the server.
  
  - sameSite (boolean|none|lax|strict): Strict or Lax enforcement