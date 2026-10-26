# Activity 6.08 — Understanding Clickjacking Attacks

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 06  
> **Class:** 23–24  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

This activity explores the concept of **Clickjacking**, a technique in which elements of a web page can be positioned over an apparently legitimate interface to trick users into clicking an element different from the one they believe they are selecting.

The exercise was performed in a laboratory environment using a local HTML page. The objective was to observe iframe behavior, change its transparency using CSS, and examine the protections available in the browser.

The laboratory did not involve attempting to perform actions on a real account or exploit a real user.

## Environment

- **Operating system:** Kali Linux
- **Access method:** RDP
- **Machine IP address:** `192.168.98.40`
- **User:** `aluno`
- **Browser:** Firefox 128.14.0esr
- **Working directory:** `/home/aluno/Documentos`

The credentials used in the laboratory are not recorded in this README.

## 1. Understanding Clickjacking

In the scenario presented by the laboratory, a malicious page could display apparently harmless content to a visitor while positioning a transparent iframe containing another website over a clickable area.

The conceptual idea is:

```text
User
   │
   │ believes they are clicking:
   ▼
[ Visible Button ]
   │
   │
   └──────► element overlapped by an iframe
                         │
                         ▼
                  Embedded content
```

Using CSS, an iframe can be positioned over other page elements, and its opacity can be adjusted.

## 2. Create the HTML Page

Mousepad was used to create a laboratory HTML page.

The content used was:

```html
<!doctype html>
<html>

<head>
  <meta charset="UTF-8">
</head>

<body>

  <style>
    iframe {
      width: 400px;
      height: 100px;
      position: absolute;
      top: 5px;
      left: -14px;
      opacity: 1;
      z-index: 1;
    }
  </style>

  <div>Click to get rich now:</div>

  <!-- The url from the victim site -->
  <iframe src="https://www.facebook.com"></iframe>

  <button>Click here!</button>

  <div>...And you're cool (I'm a cool hacker actually)!</div>

</body>
</html>
```

The file was saved as:

```text
/home/aluno/Documentos/teste.html
```

When saving the file in Mousepad, the **All Files** option was selected to retain the `.html` extension.

## 3. Open the Page in the Browser

The `teste.html` file was located using Thunar and opened in Firefox.

In the initial configuration:

```css
opacity: 1;
```

the content embedded by the iframe remained visible, initially appearing as a black rectangle on the page.

## 4. Make the Iframe Transparent

The following value:

```css
opacity: 1;
```

was changed to:

```css
opacity: 0;
```

After saving the file and reloading the page, the iframe content was no longer visually visible, while the page text and button remained displayed.

This demonstrates how the CSS `opacity` property changes an element's visibility without necessarily removing the element from the page.

## 5. Test the Interaction

A test was performed by clicking the button displayed on the page.

The browser did not allow the click to perform the expected action through the embedded content.

The laboratory scenario therefore did not work as an effective clickjacking exploit.

**Technical note:** A website may prevent itself from being embedded by sending response headers such as `X-Frame-Options` or a Content Security Policy using `frame-ancestors`. The observed behavior alone does not establish whether the restriction came from Firefox itself or from the embedded website's anti-framing policy.

## 6. Test Partial Opacity

The property value was changed again:

```css
opacity: 0;
```

to:

```css
opacity: 0.5;
```

After saving and reloading the page, the embedded element became partially visible.

Even with this configuration, the expected behavior was not achieved in Firefox during the laboratory exercise.

This illustrates the visual effect of adjusting the opacity of an iframe, although reducing opacity alone does not make a clickjacking scenario functional.

## 7. Make the Iframe Almost Invisible

The opacity was changed once more:

```css
opacity: 0.5;
```

to:

```css
opacity: 0.03;
```

After saving and reloading the page, the iframe became almost invisible, while the page elements continued to resemble a normal interface.

This step visually demonstrates one characteristic associated with clickjacking: an overlaid element can remain part of the page structure even when the user can barely see it.

## 8. Browser Protection

During the tests, the scenario did not operate as an effective exploit.

This is important because clickjacking does not depend only on the HTML and CSS used. Modern browsers and websites may apply protections that restrict embedded content or framing behavior.

For example, anti-framing response headers can prevent a website from being embedded in an iframe. The exact cause of the observed behavior would require inspecting the relevant browser console messages and HTTP response headers.

## 9. Display Only the Frame Content

To view the embedded content directly, the Firefox context menu was used:

```text
Right-click
        ↓
This Frame
        ↓
Show Only This Frame
```

This action caused the browser to display only the content of the selected frame.

This is the step used as evidence for the activity.

## Concepts Practiced

### Clickjacking

Clickjacking is a technique based on overlapping page elements to make user interaction occur on a different element from the one the user believes they are selecting.

A typical scenario may use:

- An iframe.
- Absolute positioning with CSS.
- Transparency controls.
- Overlapping elements.
- A misleading visual interface.

### Iframe

The HTML element:

```html
<iframe src="https://www.facebook.com"></iframe>
```

allows external content to be embedded within an HTML page.

In this laboratory, it was used to demonstrate the concept of content overlay.

### `opacity`

The CSS property:

```css
opacity
```

controls an element's transparency.

The following values were used in the activity:

```css
opacity: 1;
```

```css
opacity: 0.5;
```

```css
opacity: 0.03;
```

The lower the value, the more transparent the element becomes. A value of `0` makes the element fully transparent visually, but does not automatically remove it from the page or disable its interaction.

### `z-index`

The property:

```css
z-index: 1;
```

defines an element's stacking position relative to other elements in the applicable stacking context.

Combined with `position: absolute`, it can be used to position elements over other content.

## Results

The activity allowed the following behaviors to be observed in a controlled environment:

- The basic structure of an HTML page containing an iframe.
- Positioning embedded content.
- The effect of the CSS `opacity` property.
- The behavior of an almost invisible element.
- The browser's handling of the embedded website.
- Viewing the content of a frame separately.

The test did not produce a functional exploit against the embedded website. The expected behavior was blocked or otherwise unavailable in the laboratory, illustrating the importance of browser and website framing protections.

## Cleanup

After completing the tests, Firefox, Mousepad, and Thunar were closed.

In the terminal, the file created for the laboratory was removed:

```bash
sudo -i
cd /home/aluno/Documentos
rm teste.html
```

The RDP session was ended, and the virtual machine used in the laboratory was shut down.

## Evidence

The activity evidence corresponds to Step 9, showing the **This Frame → Show Only This Frame** option used to display the frame content separately.

[View Evidence — Classes 23–24](../evidencias.pdf)

---

[Back to Classes 23–24](../) · [Back to Module 06](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
