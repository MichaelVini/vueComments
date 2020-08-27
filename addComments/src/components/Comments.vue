<template>
    <div class="container">
        <h1>Comentários</h1>
            <hr />
        <div class="form-todo form-group">
            <p>
                <input placeholder="Nome" type="text" name="author" v-model="name" class="form-control" />
            </p>
            <p>
                <textarea placeholder="Comentário" name="message" v-model="message" class="form-control"></textarea>
            </p>
                <button v-on:click.prevent="addComment" type="submit" class="btn btn-primary">Comentar</button>
        </div>
        <div class="list-group-item" v-for="(comment, index) in allComments" :key="comment.message">
            <span class="comment_author"> Autor: <strong>{{ comment.name }}</strong></span>
            <p> {{ comment.message }}</p>
            <div>
                <a href="#" title="Excluir" v-on:click.prevent="deleteComment(index)">Excluir</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            comments: [],
            name: '',
            message: ''
        }
    },
    methods: {
         addComment() {
            if(this.message.trim() === ''){
                return;
            }

            this.comments.push({
                name: this.name,
                message: this.message
            });
            this.name = '';
            this.message = '';
        },
        deleteComment(index){
            this.comments.splice(index, 1);
        }
    },
    computed: {
        allComments() {
            return (
                this.comments.map((comment) => ({
                    ...comment,
                    name: comment.name.trim() === '' ? 'Anônimo' : comment.name 
                }))
            );
        }
    }
}        
</script>

<style scoped>
    .container{
        max-width: 960px;
        padding: 40px 20px;
    }

    .container hr {
        width: 600px;
        margin-left: 0;
    }

    .form-todo {
        max-width: 600px;
    }

    .list-group-item {
        margin-top: 15px;
        border: 1px solid rgba(0,0,0,.125);
    }

</style>>
    
