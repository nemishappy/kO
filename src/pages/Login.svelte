<script>
  let username = "";
  let password = "";
  let error = "";
  import { user, pages } from "../store.js";
  const onLogin = async () => {
    error = "";
    if (!(username && password)) {
      error = "plz check username and password";
      return
    }
    let res = await fetch("http://localhost:1234/api/user/login", {
      method: "POST",
      body: JSON.stringify({ username, password }),
      headers: {
        "content-type": "application/json"
      }
    });
    let text = await res.text();
    if (res.ok) {
      $user.username = username;
      $pages = "Posts";
    } else {
      error = text;
    }
  };
  const gotoReg = () => {
    $pages = "Reg";
  };
</script>

<style>
  .container {
    position: relative;
    top: 50%;
    transform: translateY(-50%);
    text-align: center;
    display: block;
  }
  .container input {
    width: 500px;
  }
  .reg {
    color: purple;
  }
  .reg:hover {
    cursor: pointer;
  }
</style>

<svelte:head>
  <title>Login to forum</title>
</svelte:head>
<section class="container">
  <div>
    <input bind:value={username} type="text" placeholder="username" />
  </div>
  <div>
    <input bind:value={password} type="password" placeholder="password" />
  </div>
  <p>
    Don't have account ?
    <span class="reg" on:click={gotoReg}>
      <!--อยากให้กดได้อ่า-->
      <strong>Register now</strong>
      
    </span>
  </p>
  {#if error}
    <p style="color:red">{error}</p>
  {/if}
  <button class="button button-outline" on:click={onLogin}>Login</button>
</section>
