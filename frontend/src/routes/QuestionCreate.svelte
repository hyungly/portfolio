<script>
    import { push } from 'svelte-spa-router'
    import fastapi from "../lib/api"
    import Error from "../components/Error.svelte"

    let error = {detail:[]}
    let subject = ''
    let content = ''

    function post_question(event) {
        event.preventDefault()
        //다음 항목을 추가
        let formData = new FormData()
        formData.append('subject', subject)
        formData.append('content', content)
        //#1
        let url = "/api/question/create"
        let params = {
            subject: subject,
            content: content,
        }

        fastapi('post', url, params, 
            (json) => {
                push("/")
            },
            (json_error) => {
                error = json_error
            }
        )
    }

    //다음 항목을 추가
    function handlePaste(event) {
        const paste = (event.clipboardData || window.clipboardData).getData('text')

        content += paste
    }
    //#2
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