<!--
# Browser support
-->
# 브라우저 지원

<!--
Angular supports most recent browsers. This includes the following specific versions:
-->
Angular는 대부분의 브라우저를 지원합니다. 좀 더 자세하게 설명하면 다음 버전을 지원합니다:

<table>

  <tr>

<th>
      <!--
      Browser
      -->
      브라우저
</th>

<th>
      <!--
      Supported versions
      -->
      지원 버전
</th>

  </tr>

  <tr>

    <td>
      Chrome
    </td>

    <td>
      <!--
      latest
      -->
      최신 버전
    </td>
  </tr>

  <tr>

    <td>
      Firefox
    </td>

    <td>
      <!--
      latest
      -->
      최신 버전
    </td>
  </tr>

  <tr>

    <td>
      Edge
    </td>

    <td>
      <!--
      2 most recent major versions
      -->
      최근 2개 메이저 버전
    </td>
  </tr>
  <tr>
    <td>
      IE
    </td>
    <td>
      11, 10, 9 ("compatibility view" mode not supported)
    </td>
  </tr>
 <tr>
   <tr>
    <td>
      IE Mobile
    </td>
    <td>
      11
    </td>
  </tr>
 <tr>
    <td>
      Safari
    </td>

    <td>
      <!--
      2 most recent major versions
      -->
      최근 2개 메이저 버전
    </td>
  </tr>
  <tr>
    <td>
      iOS
    </td>

    <td>
      <!--
      2 most recent major versions
      -->
      최근 2개 메이저 버전
    </td>
  </tr>
  <tr>
    <td>
      Android
    </td>

    <td>
      X (10.0), Pie (9.0), Oreo (8.0), Nougat (7.0)
    </td>
  </tr>

</table>

<div class="alert is-helpful">

<!--
Angular's continuous integration process runs unit tests of the framework on all of these browsers for every pull request,
using <a href="https://saucelabs.com/">SauceLabs</a> and
<a href="https://www.browserstack.com">Browserstack</a>.
-->
Angular는 <a href="https://saucelabs.com/">SauceLabs</a>와 <a href="https://www.browserstack.com">Browserstack</a>과 함께 브라우저 지원을 위해 지속적으로 노력하고 있습니다.

</div>

{@a polyfills}
<!--
## Polyfills
-->
## 폴리필 (Polyfills)

<!--
Angular is built on the latest standards of the web platform.
Targeting such a wide range of browsers is challenging because they do not support all features of modern browsers.
You compensate by loading polyfill scripts ("polyfills") for the browsers that you must support.
The [table below](#polyfill-libs) identifies most of the polyfills you might need.
-->
Angular는 최신 웹 플랫폼 표준을 준수하며 만들어졌습니다.
하지만 최신 브라우저들이 대부분 지원하는 기능을 제대로 지원하지 않는 일부 브라우저에서는 Angular 애플리케이션의 기능 중 일부가 제대로 동작하지 않을 수 있습니다.
이 문제는 폴리필 스크립트를 로드하는 방법으로 해결할 수 있습니다.
개발자들이 자주 사용하는 폴리필은 [아래 표](#polyfill-libs)를 참고하세요.

<div class="alert is-important">

<!--
The suggested polyfills are the ones that run full Angular applications.
You may need additional polyfills to support features not covered by this list.
Note that polyfills cannot magically transform an old, slow browser into a modern, fast one.
-->
이 문서에서 소개하는 폴리필은 Angular 애플리케이션을 제대로 동작시키기 위해 필요한 것들입니다.
그래서 필요한 기능이 더 있다면 또 다른 폴리필을 추가해야 할 수도 있습니다.
다만, 오래되고 느린 브라우저에 폴리필을 사용했다고 해서 최신 스펙으로 동작하고 속도도 빠른 브라우저로 짠 변신하는 것은 아닙니다.

</div>

In Angular CLI version 8 and higher, applications are built using *differential loading*, a strategy where the CLI builds two separate bundles as part of your deployed application.

* The first bundle contains modern ES2015 syntax, takes advantage of built-in support in modern browsers, ships less polyfills, and results in a smaller bundle size.

* The second bundle contains code in the old ES5 syntax, along with all necessary polyfills. This results in a larger bundle size, but supports older browsers.

This strategy allows you to continue to build your web application to support multiple browsers, but only load the necessary code that the browser needs.
For more information about how this works, see [Differential Loading](guide/deployment#differential-loading) in the [Deployment guide](guide/deployment).

## Enabling polyfills with CLI projects

The [Angular CLI](cli) provides support for polyfills.
If you are not using the CLI to create your projects, see [Polyfill instructions for non-CLI users](#non-cli).

When you create a project with the `ng new` command, a `src/polyfills.ts` configuration file is created as part of your project folder.
This file incorporates the mandatory and many of the optional polyfills as JavaScript `import` statements.

* The npm packages for the [_mandatory_ polyfills](#polyfill-libs) (such as `zone.js`) are installed automatically for you when you create your project with `ng new`, and their corresponding `import` statements are already enabled in the `src/polyfills.ts` configuration file.

* If you need an _optional_ polyfill, you must install its npm package, then uncomment or create the corresponding import statement in the `src/polyfills.ts` configuration file.

For example, if you need the optional [web animations polyfill](http://caniuse.com/#feat=web-animation), you could install it with `npm`, using the following command (or the `yarn` equivalent):

<!--
<code-example language="sh" class="code-shell">
  # install the optional web animations polyfill
  npm install --save web-animations-js
</code-example>
-->

You can then add the import statement in the `src/polyfills.ts` file.
For many polyfills, you can simply un-comment the corresponding `import` statement in the file, as in the following example.

<!--
<code-example header="src/polyfills.ts">
  /**
  * Required to support Web Animations `@angular/platform-browser/animations`.
  * Needed for: All but Chrome, Firefox and Opera. http://caniuse.com/#feat=web-animation
  **/
  import 'web-animations-js';  // Run `npm install --save web-animations-js`.
</code-example>
-->
<code-example header="src/polyfills.ts">
  /**
  * `@angular/platform-browser/animations` 패키지로 웹 애니메이션을 사용할 때 필요합니다.
  * Chrome, Firefox, Opera를 제외한 브라우저에 필요합니다. http://caniuse.com/#feat=web-animation
  **/
  import 'web-animations-js';  // `npm install --save web-animations-js` 명령을 실행한 후에 동작합니다.
</code-example>

If the polyfill you want is not already in `polyfills.ts` file, add the `import` statement by hand.


{@a polyfill-libs}

<!--
### Mandatory polyfills
-->
### 필수 폴리필

<!--
These are the polyfills required to run an Angular application on each supported browser:
-->
다음 브라우저에서 Angular 애플리케이션을 실행하려면 반드시 폴리필을 적용해야 합니다:

<table>

  <tr style="vertical-align: top">

    <th>
      <!--
      Browsers (Desktop & Mobile)
      -->
      브라우저 (데스크탑 & 모바일)
    </th>

    <th>
      <!--
      Polyfills Required
      -->
      필요한 폴리필
    </th>

  </tr>

  <tr style="vertical-align: top">

    <td>
      Chrome, Firefox, Edge, <br>
      Safari, Android, IE 10+
    </td>

    <td>

      [ES2015](guide/browser-support#core-es6)

    </td>

  </tr>

  <tr style="vertical-align: top">

    <td>
      IE 9
    </td>

    <td>

      ES2015<br>[classList](guide/browser-support#classlist)

    </td>

  </tr>

</table>


<!--
### Optional browser features to polyfill
-->
### 폴리필을 적용해야 하는 Angular 기능

<!--
Some features of Angular may require additional polyfills.
-->
Angular 기능 중 일부는 폴리필을 추가로 적용해야 하는 것이 있습니다.

<table>

  <tr style="vertical-align: top">

    <th>
      <!--
      Feature
      -->
      기능
    </th>

    <th>
      <!--
      Polyfill
      -->
      폴리필
    </th>

    <th style="width: 50%">
       <!--
       Browsers (Desktop & Mobile)
       -->
       브라우저 (데스크탑 & 모바일)
    </th>

  </tr>

  <tr style="vertical-align: top">

    <td>

      [AnimationBuilder](api/animations/AnimationBuilder).
      (Standard animation support does not require polyfills.)

    </td>

    <td>

      <!--
      [Web Animations](guide/browser-support#web-animations)
      -->
      [웹 애니메이션](guide/browser-support#web-animations)

    </td>

    <td>
      <p>If AnimationBuilder is used, enables scrubbing
      support for IE/Edge and Safari.
      (Chrome and Firefox support this natively).</p>
    </td>

  </tr>

  <tr style="vertical-align: top">

    <td>

       <!--
       [NgClass](api/common/NgClass) on SVG elements
       -->
       SVG 엘리먼트에 적용하는 [NgClass](api/common/NgClass) 
    </td>

    <td>

      [classList](guide/browser-support#classlist)

    </td>

    <td>
      IE 10, IE 11
    </td>

  </tr>

  <tr style="vertical-align: top">

    <td>

      <!--
      [Http](guide/http) when sending and receiving binary data
      -->
      [Http](guide/http)를 사용해서 바이너리 데이터를 보내거나 받을 때
    </td>

    <td>

      [Typed&nbsp;Array](guide/browser-support#typedarray)<br>

      [Blob](guide/browser-support#blob)<br>

      [FormData](guide/browser-support#formdata)

    </td>

    <td>
      IE 9
    </td>

  </tr>

  <tr style="vertical-align: top">

    <td>

      [Router](guide/router) when using
      [hash-based routing](guide/router#appendix-locationstrategy-and-browser-url-styles)
    </td>

    <td>

      [ES7/array](guide/browser-support#core-es7-array)

    </td>

    <td>
      IE 11
    </td>

  </tr>

</table>



<!--
### Suggested polyfills
-->
### 추천 폴리필

The following polyfills are used to test the framework itself. They are a good starting point for an application.


<table>

  <tr>

    <th>
      <!--
      Polyfill
      -->
      폴리필
    </th>

    <th>
      <!--
      License
      -->
      라이센스
    </th>

    <th>
      <!--
      Size*
      -->
      크기*
    </th>

  </tr>

  <tr>

    <td>

      <a id='core-es7-array' href="https://github.com/zloirock/core-js/tree/v2/fn/array">ES7/array</a>

    </td>

    <td>
      MIT
    </td>

    <td>
      0.1KB
    </td>

  </tr>

  <tr>

    <td>

      <a id='core-es6' href="https://github.com/zloirock/core-js">ES2015</a>

    </td>

    <td>
      MIT
    </td>

    <td>
      27.4KB
    </td>

  </tr>

  <tr>

    <td>

      <a id='classlist' href="https://github.com/eligrey/classList.js">classList</a>

    </td>

    <td>
      Public domain
    </td>

    <td>
      1KB
    </td>

  </tr>

  <tr>

    <td>

      <a id='intl' href="https://github.com/andyearnshaw/Intl.js">Intl</a>

    </td>

    <td>
      MIT / Unicode license
    </td>

    <td>
      13.5KB
    </td>

  </tr>

  <tr>

    <td>

       <a id='web-animations' href="https://github.com/web-animations/web-animations-js">Web Animations</a>

    </td>

    <td>
      Apache
    </td>

    <td>
      14.8KB
    </td>

  </tr>

  <tr>

    <td>

      <a id='typedarray' href="https://github.com/inexorabletash/polyfill/blob/master/typedarray.js">Typed Array</a>

    </td>

    <td>
      MIT
    </td>

    <td>
      4KB
    </td>

  </tr>

  <tr>

    <td>

       <a id='blob' href="https://github.com/eligrey/Blob.js">Blob</a>

    </td>

    <td>
      MIT
    </td>

    <td>
      1.3KB
    </td>

  </tr>

  <tr>

    <td>

       <a id='formdata' href="https://github.com/francois2metz/html5-formdata">FormData</a>

    </td>

    <td>
      MIT
    </td>

    <td>
      0.4KB
    </td>

  </tr>

</table>

<!--
\* Figures are for minified and gzipped code,
computed with the <a href="http://closure-compiler.appspot.com/home">closure compiler</a>.
-->
\* <a href="http://closure-compiler.appspot.com/home">closure compiler</a>로 압축되고 난독화된 크기입니다.

{@a non-cli}

<!--
## Polyfills for non-CLI users
-->
## Angular CLI를 사용하지 않는 경우에 필요한 폴리필

If you are not using the CLI, add your polyfill scripts directly to the host web page (`index.html`).

For example:

<!--
<code-example header="src/index.html" language="html">
  &lt;!-- pre-zone polyfills -->
  &lt;script src="node_modules/core-js/client/shim.min.js">&lt;/script>
  &lt;script src="node_modules/web-animations-js/web-animations.min.js">&lt;/script>
  &lt;script>
    /**
     * you can configure some zone flags which can disable zone interception for some
     * asynchronous activities to improve startup performance - use these options only
     * if you know what you are doing as it could result in hard to trace down bugs..
     */
    // __Zone_disable_requestAnimationFrame = true; // disable patch requestAnimationFrame
    // __Zone_disable_on_property = true; // disable patch onProperty such as onclick
    // __zone_symbol__UNPATCHED_EVENTS = ['scroll', 'mousemove']; // disable patch specified eventNames

    /*
     * in IE/Edge developer tools, the addEventListener will also be wrapped by zone.js
     * with the following flag, it will bypass `zone.js` patch for IE/Edge
     */
    // __Zone_enable_cross_context_check = true;
  &lt;/script>
  &lt;!-- zone.js required by Angular --&gt;
  &lt;script src="node_modules/zone.js/dist/zone.js">&lt;/script>

  &lt;!-- application polyfills --&gt;
</code-example>
-->
<code-example header="src/index.html" language="html">
  &lt;!-- 폴리필에 필요한 스크립트 --&gt;
  &lt;script src="node_modules/core-js/client/shim.min.js">&lt;/script>
  &lt;script src="node_modules/web-animations-js/web-animations.min.js">&lt;/script>
  &lt;script>
    /**
     * 애플리케이션 초기 실행 시간을 줄이려면 zone에 관련된 플래그들을 비활성화할 수 있습니다.
     * 이 옵션을 사용하면 디버깅이 어려워지기 때문에 관련 내용을 확실하게 이해하고 있을 때만 적용하세요.
     */
    // __Zone_disable_requestAnimationFrame = true; // requestAnimationFrame 패치를 비활성화합니다.
    // __Zone_disable_on_property = true; // onclick과 같은 onProperty 패치를 비활성화합니다.
    // __zone_symbol__BLACK_LISTED_EVENTS = ['scroll', 'mousemove']; // 이벤트 이름으로 동작하는 패치를 비활성화합니다.

    /*
     * IE/Edge 개발자 도구에서는 addEventListener가 zone.js을 사용합니다.
     * 아래 옵션을 설정하면 IE/Edge에서 `zone.js` 패치를 생략할 수 있습니다.
     */
    // __Zone_enable_cross_context_check = true;
  &lt;/script>
  &lt;!-- Angular에는 zone.js이 필요합니다. --&gt;
  &lt;script src="node_modules/zone.js/dist/zone.js">&lt;/script>

  &lt;!-- 애플리케이션 폴리필 --&gt;
</code-example>