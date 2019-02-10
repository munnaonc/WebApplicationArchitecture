<h1>Monolithic WebApp With Scalability</h1>
<img src='https://github.com/munnaonc/webapplicationarchitecture/blob/master/webapparchitecture.png'>
<a href='https://github.com/munnaonc/webapplicationarchitecture/blob/master/MonolithicWebAppWithScalability.pdf'>Download the PDF</a>
<p>Community Recognision : The above diagram is created using [www.draw.io] a free tool to design awesome diagram.</p>

<p>A brief description of the above application architecture is given below.</p>

<h3>Presentations Layer</h3>

<p>a) Single page application or traditional MVC web app:  Regardless of the application type the presentation layer consists of feature modules which in turn contains component and component logic (which may be separated in one or more javascript class).</p>

<p>b) The components in the presentation layer shall access (public or "site of origin" api via the javascript proxy layer. ( validation of XSR, anti-forgery token, bearer token etc shall be handled in the javascript resource access layer). Http Interceptors which are catered for custom need will also be added here.</p>

<p>c) The application may or may not have cross-cutting UI concerns which include, common components, shared utility classes.</p>

<h3>Cloud Cache</h3>

<p>The application may choose to cache any static resource files in any content delivery network to delegate static resource availability, performance, and bandwidth optimization. Example resource could be bootstrap javascript and CSS files, custom minified CSS files, globalization supported javascript resource files, translation files to support multi-language.</p>

<h3>Server Applications</h3>

<p>a) The web application must have a server site/app which may be developed with any modern MVC web app architecture ( Model/View/Controllers). </p>

<p>The authentication and authorization must be handled at this layer. The web app may choose to implement, custom membership or OpenID connect/SAML2.0 to implement single sign-on.</p>

<p>MVC Controller layer will have the behaviors to support the application view biding and actions which includes the allowed HTTP verbs. (HTTP get, HTTP post, and HTTP redirect [OpenIdConnect and SMAL2.0])</p>

<p>b) A REST Web api should be available for rich client functionality, where the web api may reside within the site of origin or in a separate application (bearer token, refresh token must be implemented to support separate application).</p>

<p>c) The web app may choose to expose a legacy ASMX or WCF service to support their Legacy application which requires access to the data.</p>

<h3>Common Backend</h3>

<p>a) Data access layer: Common backend must contain data access classes to retrieve and save data to and from the database. (EF 6, Ado.net or Any ORM)</p>

<p>b) Business access layer:  The business logic layer will consist of logic classes to validate business logic, security concerns, licensing concerns. Business logic classes will filter out data before making an attempt to save the data. For the complex transaction, the business layer would create transactions to complete a successful operation or rollback the operation changes. </p>

<p>c) Service Layer: Service layer would be a common and unified layer which will be a facade for the business logic, the service layer shall be consumed by the service side deliverables (asp.net MVC app, asp.net web app, WCF app etc).</p>

<p>d) Cross-cutting concerns: The cross-cutting concerns are consists of DTO ( Data transfer objects) (aka: Model classes), BO( Business object, contains business object validations), Utility methods, Security check (Role security, Resource Security) and others generic cross-cutting concerns. This groups of objects will be shared across all the layer and applications.</p>

<p>e) Audit/Logging: Audit logs and exception log may be maintained via (Net4Log or slunk) proper logging layer.</p>

<h3>Other Services (Async Processing Services)</h3>

<p>a) Notification Service: The application may require to generate report, notification, alerts etc, which may be sent via email, SMS using Some services (windows). (MSMQ or RabitMQ or another [X]MQ will be used to delegate the application load to scale better. </p>



