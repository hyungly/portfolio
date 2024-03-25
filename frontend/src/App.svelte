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
	import { clickOutside } from './click_outside.js';

	let showModal = true;

  const routes = {
    '/': Home,
    '/detail/:question_id': Detail,
    '/question-create': QuestionCreate,
    '/user-create': UserCreate,
    '/user-login': UserLogin,
    '/question-modify/:question_id': QuestionModify,
    '/answer-modify/:answer_id': AnswerModify,
  }
</script>

<button on:click={() => (showModal = true)}>Show Modal</button>
{#if showModal}
	<div class="box" use:clickOutside on:outclick={() => (showModal = false)}>Minboard 방문을 환영합니다!</div>
{/if}

<style>
	.box {
		--width: 225px;
		--height: 45px;
		position: absolute;
		width: var(--width);
		height: var(--height);
		left: calc(50% - var(--width) / 2);
		top: calc(50% - var(--height) / 2);
		display: flex;
		align-items: center;
		padding: 8px;
		border-radius: 4px;
		background-color: #727272da;
		color: #0000009a;
		text-align: center;
		font-weight: bold;
	}
</style>

<Navigation />
<Router {routes}/>