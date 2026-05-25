# Introduction

In the previous lesson, we explored the basics of CSS and how it can be used to style HTML elements directly within the element itself. This method, where styles are applied directly within the HTML tag, is known as **inline CSS**. While inline CSS is useful for quick, specific changes, there are more powerful and flexible ways to apply CSS to your web projects. In this lesson, we will explore the different methods of including CSS, understand when to use each method, and introduce the concept of how CSS rules interact with one another.

# Three Ways to Include CSS

CSS can be applied to your HTML documents in three primary ways: **Inline CSS**, **Internal CSS**, and **External CSS**. Each method serves different purposes and can be used depending on your project's needs.

### **1\. Inline CSS**

Inline CSS is applied directly within an HTML element using the style attribute. This method is useful for quick, specific changes but is generally **not** recommended for large projects due to its limitations in reusability and maintenance.

**Example of Inline CSS:**

`<p style="color: blue; font-size: 18px;">This is a paragraph with inline CSS.</p>
`

### **2\. Internal CSS**

Internal CSS is defined within a `<style></style>` tag inside the `<head></head>` section of your HTML document. This method is particularly useful when you need to apply styles to a single HTML page without affecting other pages.

### **3\. External CSS**

External CSS involves writing all your styles in a separate <kbd class="slate-kbd">.css</kbd> file, which is then linked to your HTML document using a `<link>` tag. This is the preferred method for larger projects, as it allows you to apply consistent styles across multiple pages and maintain a clean separation between your HTML content and CSS styling.

# Understanding CSS Syntax

To apply CSS effectively, it’s important to understand its syntax. CSS rules are composed of a **selector** and a **declaration block**.

```
selector {
    property: value;
}
```

- **Selector** : The selector identifies the HTML element(s) you want to style.
- **Declaration Block** : The declaration block contains one or more style declarations, each consisting of a **property** and a **value**.

Example:

```
p {
    color: blue;
    font-size: 18px;
}
```

In this example, the selector **p** targets all `<p>` (paragraph) elements in the document. The declaration block specifies that all paragraphs should have blue text and a font size of 18 pixels.

# Applying Internal and External CSS

Now that we understand the syntax, let&#x27;s see how CSS can be applied using both internal and external methods.

## Internal CSS Example:

Internal CSS is written directly within the `<style>` tag in the `<head>` section of your HTML document.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Internal CSS Example</title>
    <style>
        body {
            font-family: Arial;
            color: darkslategrey;
        }
        p {
            color: navy;
            font-size: 16px;
        }
    </style>
</head>
<body>
        <h1>This is a Heading</h1>
    <p>This paragraph is styled with internal CSS.</p>
    <p>Another paragraph, also styled the same way.</p>
</body>
</html>
```

In this example, the internal CSS applies styles to all `<p>` elements in the document, setting their color to navy and font size to 16 pixels.

## External CSS Example:

External CSS is defined in a separate file, which is linked to the HTML document.

**HTML Document:**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>External CSS Example</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>This is a Heading</h1>
    <p>This paragraph is styled with external CSS.</p>
    <p>Another paragraph, also styled the same way.</p>
</body>
</html>
```

**External CSS File (****styles.css****):**

```
body {
    font-family: Arial;
    color: darkslategrey;
}

p {
    color: navy;
    font-size: 16px;
}
```

In this example, the CSS is stored in a separate file (styles.css). The styles apply to all `<p>` elements across any HTML document that links to this CSS file.

# Which Method to Use and When?

*   **Inline CSS** is best for small, specific changes or when you need to override other styles. However, it should be used sparingly due to its lack of reusability and maintainability.
    
*   **Internal CSS** is suitable for single-page applications or when experimenting with styles on a single page during development.
    
*   **External CSS** is preferred for larger projects as it allows for centralized management of styles, reusability across multiple pages, and cleaner code structure.
    

# Understanding the Cascading Nature of CSS

The cascade is the algorithm for solving conflicts where multiple CSS rules apply to an HTML element. We will learn more about it in future sections. For now, we will only focus on two things that affect the styles applied on HTML elements:

1.  Order of appearance
    
2.  Inline vs Internal / External Stylesheets
    

## Order of Appearance

The styles are applied in the order they are encountered by the browser, from top to bottom. If the same property is defined multiple times for an element, the last one in the cascade will take precedence.

For example, if you define the **color** property for a paragraph twice, the paragraph will take on the color defined in the last rule:

```
p {
    color: blue;
}

p {
    color: red;
}
```

Here, the paragraph will be red because it’s the last color defined.

The same principle applies to the order of stylesheets. If an external stylesheet is linked after an internal stylesheet, the external styles will override the internal ones. Conversely, if the internal stylesheet appears last, its styles will take precedence:

```
<!-- External CSS linked before internal CSS -->
<link rel="stylesheet" href="styles.css">
<style>
    p {
        color: green;
    }
</style>
<!-- Paragraphs will be green due to the internal CSS coming last -->
```

The cascading nature of CSS is a powerful feature that allows for flexibility and control in how styles are applied to your web pages. By understanding and leveraging this order, you can ensure your designs look exactly as intended.

## Inline vs Internal vs External Stylesheets

When multiple CSS rules target the same element, the following order of precedence determines which styles are applied:

1.  **Inline CSS** (highest priority)
    
2.  **Internal CSS** (within a `<style>` tag, same priority as external)
3.  **External CSS** (same priority as internal)
4.  **Browser Defaults** (lowest priority)

# What Happens When CSS Rules Conflict?

When CSS rules from different sources conflict, the browser uses the order of precedence and specificity to determine which styles to apply.

For example: 

**index.html**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cascading Example</title>
    <style>
        p {
            color: green; /* Internal CSS */
        }
    </style>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <p style="color: red;">This paragraph is styled with inline CSS.</p>
</body>
</html>
```
    
**styles.css**
    
```
body {
    color: darkgrey;
}

p {
    color: navy;
}
```

The paragraph will appear in red because the inline style has the highest priority, overriding both internal and external CSS.

# Best Practices and Common Mistakes

### **Best Practices**

*   **Prefer External CSS**: Whenever possible, use external CSS to ensure your styles are centralized and reusable across multiple pages. This practice promotes cleaner code and easier maintenance.
    
*   **Be Cautious with Inline CSS**: Avoid using inline CSS unless absolutely necessary. Inline styles have the highest priority but can lead to messy, difficult-to-maintain code.
    
*   **Organize Your CSS**: Group related styles together, and use comments to separate sections in your CSS file. This organization improves readability and helps prevent errors.
    
*   **Understand Inheritance and Cascading**: Knowing how inheritance and cascading work will help you write more effective CSS and avoid conflicts.
    

### **Common Mistakes**

*   **Overusing Inline Styles**: Beginners often overuse inline styles for convenience, leading to cluttered HTML and inconsistent styling.
    
*   **Duplicating Styles**: Duplicating styles across multiple internal or inline CSS blocks can make your code harder to maintain and lead to inconsistencies.
    

# Practice Problem

You are creating a simple webpage about your favorite place. The page includes a title, a few paragraphs describing the place, and a fun fact at the end. Your task is to style this page using inline CSS, internal CSS, and an external stylesheet.

### **Starter HTML Code:**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Favorite Place</title>
</head>
<body>
    <h1>My Favorite Place</h1>
    <h2>Introduction</h2>
    <p>This place is amazing because...</p>
    <h2>Things to Do</h2>
    <p>There are many activities such as...</p>
    <h2>Fun Fact</h2>
    <p>This place has a unique feature...</p>
</body>
</html>
```

### **Instructions:**

1.  **Inline CSS:**
    
    * Change the color of the main title (`<h1>`) to **dark blue** and the font size to **36px**.
        
    * Change the background color of the "Fun Fact" paragraph (`<p>`) to **light gray**.
        
2.  **Internal CSS:**
    
    * Use internal CSS to set the text color of all paragraphs (`<p>`) to **green** and the font size to **18px**.
        
    * Set the text color of all `<h2>` elements to **dark green**.
        
3.  **External CSS:**
    
    * In an external stylesheet, set the background color of the entire page (`<body>`) to **light blue**.
        
    * Set the font family of all headings (`<h1>`,`<h2>`) to **Arial, sans-serif** and center-align the text.

### **Key Concepts:**

*   **Inheritance:** Notice how the internal CSS styles for paragraphs might be overridden by inline CSS.
    
*   **Cascading:** Observe which styles take precedence when conflicts arise between inline, internal, and external CSS.