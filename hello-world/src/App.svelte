<script>
  import { bubble } from "svelte/internal";

  const name = "chandan";
  const richName = "<b>chandan</b>";

  /* helper: just for demo */
  function getCookie(c_name) {
    return localStorage.getItem(c_name);
  }

  function setCookie(c_name, value, expiredays) {
    return localStorage.setItem(c_name, value);
  }

  const fakeUserSessionID = "secret_" + Math.random().toString(36).substring(2);
  setCookie("sessionID", fakeUserSessionID);

  /* end of helper */

  // malicious users (@dexter) gonna insert this piece of code
  // into the rich text input field in order to pass their semester
  const xssHack = `
  <a href="#" onClick="alert('sessionID: ' + localStorage.getItem('sessionID'))">
  Click to Claim Your iPhone XR Pro Max Ultra Lite!
  </a>`;

  // attribute binding
  const headingId = "heading";
  const id = "heading";
  const disabled = false;
</script>

<main>
  <h1>Hello {name}</h1>
  <h2>{@html richName}</h2>
  <h2>{@html xssHack}</h2>
  <h2 id={headingId}>Heading</h2>
  <h2 {id}>Shorthand Attribute Binding (varibale name == attribute name)</h2>
  <button {disabled}>Bind Button</button>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
