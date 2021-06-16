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
  const status = ["danger", "success"];
  const ispromoted = true
</script>

<main>
  <h1>Hello {name}</h1>
  <h2>{@html richName}</h2>
  <h2>{@html xssHack}</h2>
  <h2 id={headingId}>Heading</h2>
  <h2 {id}>Shorthand Attribute Binding (varibale name == attribute name)</h2>
  <button {disabled}>Bind Button</button>
  <!-- static class -->
  <h2 class="underline">Static Class</h2>
  <!-- dynamic classes -->
  <button class={status[0]}>Cancel</button>
  <button class={status[1]}>OK</button>
  <!-- dynamic attribute binding -->
  <h2 class={ispromoted ? "promoted" : ""}>Title</h2>
  <h2 class:promoted={ispromoted}>Dynamic Classes</h2>
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

  .underline {
    text-decoration: underline;
  }

  button {
    color: #fff;
    border: 0;
    transition: all 200ms ease-in-out;
    cursor: pointer;
  }

  .danger {
    background: red;
  }

  .success {
    background: green;
  }

  .promoted {
    font-style: italic;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
