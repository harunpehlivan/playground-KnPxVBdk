# Introduction!

ASP.NET MVC (Model-View-Controller architectural pattern) is getting popular day by day, due to Separation of code, extensive templates, data-binding, test-driven development (TDD), Scaffolding and no view state like features, it has REST and SEO support nature. it is really an plugged and extensible framework. We get complete control over HTML with MVC support.  But before going to code on ASP.NET MVC we should take care of some Do's and Dont's or best practices. Here i am explaining some Do's and Don'ts of ASP.NET MVC code

Many developers/organizations thinking of migrating their exiting application to ASP.NET MVC, This article will help them to understand code facts

## Do's and Dont's/Best Practices

![DOsDonts](http://1.bp.blogspot.com/-hYypFLqS9kU/VlV5RznNIrI/AAAAAAAABqs/qUSZu4zwBcE/s1600/Do_Dont.png)

- Business logic should be the part of Model only
Before start code on MVC we should make understand that Business logic should be reside in Model only, it will add your security and code duplication can be avoided. The view load faster as there is no business present in view.

-  Use only specific view engine
View engines are used to create HTML markup from your view, it is the combination of HTML and programming code, ASP.NET has its own asp.net engine where as ASP.NET MVC has its razor engine. You should only use your specified view engine, it will increase application performance, see below snippet 

```javascript
protected void Application_Start()
{
    ViewEngines.Engines.Clear(); //clear all engines
    ViewEngines.Engines.Add(new RazorViewEngine());
}
```

3. Create separate assembly for Model
if the application is large and complex then make separate assembly for Model to avoid An unfortunate mishap.  Basically Model should contain business logic, Validation part, session maintenance and data logic part.

4. HTML and data access part should be done from VIEW only
As we know VIEW is the presenter part and it should be very flexible. VIEW should not contains any business logic and session maintenance, use ViewData to access data in View. 

5.  Business logic and data access should not exist in ControllerViewData
Controller should be only responsible for calling model, Prepare view, return view, redirect to action etc

6. Delete Demo code from application when you create it
Delete AccountController and all other auto created code from application it will slow down the performance

7. Disable request validation
Request validation validate the request submitted to server and avoid the potential dangerous characters, but it will also block the contents to post HTML markup tags to the server, so disable it, with the help of ValidateInput we can do it, see below snippet

```javascript
[ValidateInput(false)]
[AcceptVerbs(HttpVerbs.Post)]
public ActionResult Create([Bind(Exclude="Name")]TestEmployee clsEmp)
{
//code goes here
}
```

8. Master view model may be use for Uniformness
In ASP.NET master pages are used to maintain uniformness in look and feel, same way in ASP.NET MVC we use master view for it.

9.  Data Annotations can be used for server side validation
Use System.ComponentModel.DataAnnotations namespace for server side validation, just use it in model with attribute, see snippet

```javascript
Public class GetAddress
{
    [Required(ErrorMessage="Address is mandatory")]
    public string Address { get; set; }
}
```

10. Use extension methods
Extension method help us to simplify LINQ queries and improve application performance, these methods are the static methods and access with this keyword.

11. Remove un-necessary folders and references
When you start creating new ASP.NET MVC application, visual studio does create lot of un-necessary folders and references that are not useful, we can remove them to avoid additional overhead on application

12. Do Bundling and Minifying CSS Files
Bundling and Minifying is the process of minimizing the size of referenced file like .JS, .JSON, .CSS we can reduce the size of such files which will ultimately boost the application performance, in Bundling we merge all CSS in one file and same done for .JS and .JSON file in Minification we remove extra spaces and enters from file and reduce file size

13. For each view there should be a view model
Do you have view ? if yes then create ViewModel. it should used only for data binding and may not contain any presenter code. ViewModel is essential when we want to show some data in different format, in such case view only responsible for present and ViewModel does the job of data transformation

14. Design Routing properly not URL re-writing
URL routing is very much different than URL re-writing, may developers consider them as unique thing. URL routing does not create new URL for old URL but it maps resources with route

15.  Use ViewData and ViewBag for large data storage
If you want to work with lage data, spread sheets, dashboards or volume data sources then ViewData is good option, both views and controllers can easily access ViewData and ViewBag

16. For current and the subsequent requests use TempData
TempData is very short-lived instance, it should use only For current and the subsequent requests.

17. Use Glimpse, fidder, F-12 like package to monitor and improve performance of ASP.NET MVC
Glimpse NuGet package provide detail diagnostic information of ASP.NET apps, where as fidder, F-12 shows you client side activities, more information can be found on Here

18.  Deploy code in Release mode
Code with Release is more compressed than debug mode as it does not conain .pdb file so less memory is utilized by it

19. Remove unnessary HTTP headers
Remove X-AspNetMvc version from global.asax.cs as it will not provide no direct benifit and un-necessarily use small amount of bandwidth, see below snippet

```javascript
MvcHandler.DisableMvcResponseHeader = true;
```

20. Use CDN (Content Delivery Networks)
CDN is helping you to download your supportive things (like required .JS, .CSS, .JSON files) from nearest location/server, so travelling time of resources from one location to another will save significantly.

21. Use validationSummary to show all validations in one snap
see below method to use to show all validation in one snap

```javascript
<%= Html.ValidationSummary() %>
```

22. Razor is recommended 
We know ASP.NET MVC support multiple engines but Razor is recommended by Microsoft as it is light weight and it has very simple syntax

23. Do you want some repetitive UI to be display on each page ? use Partial view
Partial view is like a user control in classic ASP.NET, you can use them if you want to show piece of UI on each page

24. If you are not using bundles and WebAPI then simple remove their associated files
Go to App_start directory and remove BundleConfig file, now go to Application_Start method, in Global.asax.cs and remove the line BundleConfig.RegisterBundles, same thing you can do for WebApiConfig

This is not a detail level document, this document at least need a basic knowledge of ASP.NET MVC, i will cover more detail documentation in next version of this document till then enjoy this stuff

Suggestion and Queries are always welcome

-Prasad