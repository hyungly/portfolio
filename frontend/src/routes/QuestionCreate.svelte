<script>
  import { push } from 'svelte-spa-router'
  import fastapi from "../lib/api"
  import Error from "../components/Error.svelte"

  let error = {detail:[]}
  let subject = ''
  let content = ''
  let imageFile = null

  function handleImageUpload(event) {
      const file = event.target.files[0]
      imageFile = file
  }

  function post_question(event) {
      event.preventDefault()

      let formData = new FormData()
      formData.append('subject', subject)
      formData.append('content', content)
      if (imageFile) {
          formData.append('image', imageFile)
      }

      let url = "/api/question/create"

      fastapi('post', url, formData, 
          (json) => {
              push("/")
          },
          (json_error) => {
              error = json_error
          }
      )
  }
</script>

<div class="container">
  <h5 class="my-3 border-bottom pb-2">글쓰기</h5>
  <Error error={error} />
  <form method="post" class="my-3">
      <div class="mb-3">
          <label for="subject">제목</label>
          <input type="text" class="form-control" bind:value="{subject}">
      </div>
      <div class="mb-3">
          <label for="content">내용</label>
          <textarea class="form-control" rows="10" bind:value="{content}"></textarea>
      </div>
      <div class="mb-3">
          <label for="imageUpload">이미지 첨부</label>
          <input type="file" id="imageUpload" accept="image/*" on:change={handleImageUpload}>
      </div>
      <button class="btn btn-primary" on:click="{post_question}">작성하기</button>
  </form>
</div>
