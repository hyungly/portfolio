<script>
  import Router from 'svelte-spa-router'
  import Home from "./routes/Home.svelte"
  import Detail from "./routes/Detail.svelte"
  import QuestionCreate from "./routes/QuestionCreate.svelte"
  import Navigation from "./components/Navigation.svelte"
  import UserCreate from "./routes/UserCreate.svelte"
  import UserLogin from "./routes/UserLogin.svelte"
  import QuestionModify from "./routes/QuestionModify.svelte"
  import AnswerModify from "./routes/AnswerModify.svelte"

  const routes = {
    '/': Home,
    '/detail/:question_id': Detail,
    '/question-create': QuestionCreate,
    '/user-create': UserCreate,
    '/user-login': UserLogin,
    '/question-modify/:question_id': QuestionModify,
    '/answer-modify/:answer_id': AnswerModify,
  }
  
  let hereKitty = false;

  const handleMouseenter = () => (hereKitty = true);
  const handleMouseleave = () => (hereKitty = false);

</script>

<svelte:body on:mouseenter={handleMouseenter} on:mouseleave={handleMouseleave} />

<img
  class:curious={hereKitty}
  alt="Kitten wants to know what's going on"
  src="src\routes\image\kitten.png"
  style="width: 15%;"
/>

<style>
  img {
      position: absolute;
      left: 0;
      bottom: -60px;
      transform: translate(-80%, 0) rotate(-30deg);
      transform-origin: 100% 100%;
      transition: transform 0.4s;
  } 

  .curious {
      transform: translate(-15%, 0) rotate(0deg);
  }

  :global(body) {
      overflow: hidden;
  }
</style>

<Navigation />
<Router {routes}/>