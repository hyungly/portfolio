<script>
    import { push } from 'svelte-spa-router'
    import fastapi from "../lib/api"
    import Error from "../components/Error.svelte"

    let error = {detail:[]}
    let subject = ''
    let content = ''
    let photo = null

    function post_question(event) {
        event.preventDefault()
        
        let formData = new FormData()
        formData.append('subject', subject)
        formData.append('content', content)
        formData.append('photo', photo) // 첨부된 사진 추가

        let url = "/api/question/create"

        fastapi('post', url, params, 
            (json) => {
                push("/")
            },
            (json_error) => {
                error = json_error
            }
        )
    }
    function handlePaste(event) {
        const paste = (event.clipboardData || window.clipboardData).getData('text')
        
        content += paste
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
        <button class="btn btn-primary" on:click="{post_question}">작성하기</button>
    </form>
</div>