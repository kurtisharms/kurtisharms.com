---
title: "Contact me"
template: "page"
---

Please send me a message using the form below and I will read and respond as soon as possible.

<!-- Sources:
  https://www.netlify.com/docs/form-handling/
  https://codebushi.com/form-handling-gatsby-netlify/
  https://www.netlify.com/blog/2017/07/20/how-to-integrate-netlifys-form-handling-in-a-react-app/
 -->
<form name="contact" method="post" action="/pages/contact-success" data-netlify="true" data-netlify-honeypot="bot-field">
  <input type="hidden" name="form-name" value="contact" />
  <p style="display:none;">
    <label>Don’t fill this out if you're human: <input name="bot-field" /></label>
  </p>
  <p>
    <input type="text" name="name" placeholder="Your Name" /> 
  </p>
  <p>
    <input type="email" name="email" placeholder="Your email" />
  </p>
  <p>
    <label>Message <br />
    <textarea name="message" style="width:100%;height:300px;"></textarea></label>
  </p>
  <p>
    <button type="submit">Send</button>
  </p>
</form>

<!-- Morbi in sem quis dui placerat ornare. Pellentesque odio nisi, euismod in, pharetra a, ultricies in, diam. Sed arcu. Cras consequat.

Mauris placerat eleifend leo. Quisque sit amet est et sapien ullamcorper pharetra. Vestibulum erat wisi, condimentum sed, commodo vitae, ornare sit amet, wisi. Aenean fermentum, elit eget tincidunt condimentum, eros ipsum rutrum orci, sagittis tempus lacus enim ac dui.

![Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo. Quisque sit amet est et sapien ullamcorper pharetra. Vestibulum erat wisi, condimentum sed, commodo vitae, ornare sit amet, wisi.](/media/image-4.jpg)

*Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo. Quisque sit amet est et sapien ullamcorper pharetra. Vestibulum erat wisi, condimentum sed, commodo vitae, ornare sit amet, wisi.*

## Header Level 2

Praesent dapibus, neque id cursus faucibus, tortor neque egestas augue, eu vulputate magna eros eu erat. Aliquam erat volutpat. Nam dui mi, tincidunt quis, accumsan porttitor, facilisis luctus, metus.

+ **Lorem ipsum** dolor sit amet, consectetuer adipiscing elit.
+ Aliquam tincidunt mauris eu risus.
+ Vestibulum auctor dapibus neque.

### Header Level 3

Phasellus ultrices nulla quis nibh. Quisque a lectus. Donec **consectetuer** ligula vulputate sem tristique cursus. Nam nulla quam, gravida non, commodo a, sodales sit amet, nisi.

Pellentesque fermentum dolor. Aliquam quam lectus, facilisis auctor, ultrices ut, elementum vulputate, nunc.

#### Header Level 4

Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. -->