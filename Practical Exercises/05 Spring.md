Spring Initialiser
---------------

Download a Spring template project with the following dependencies

- Web
- DevTools
- Thymeleaf

from [https://start.spring.io/](https://start.spring.io/)

Unzip in a directory of your choice.



Add Controller
---------

Create a new class in the same package of the `@SpringBootApplication` and annotate as `@Controller`.

Implement a method with `String` return type that takes an argument of type `Model`. Annotate with `@GetMapping("/")`.
Return a String literal `index` as the name of the template to be rendered. On the model instance call `model.addAttribute("time", new Date());`

Add Template
---------
In the directory `java/resources/templates` add a file `index.html` with the following contents:
```html
<!DOCTYPE html>
<html lang="en" xmlns="http://www.w3.org/1999/xhtml"
      xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>SPE Lab</title>
</head>
<body>
<h1>Hello!</h1>
<p>The time is <span th:text="${time}"/></p>
</body>
</html>
```

This is mainly plain HTML except for the line `<p>The time is <span th:text="${time}"/></p>`.

Run 
---

Run with `mvn spring-boot:run`
