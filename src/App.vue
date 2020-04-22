<template>
    <div id="app">
        <b-input-group
                size="sm"
                class="mb-3"
        >
            <b-form-input v-model="owner_id" placeholder="введите id"></b-form-input>
            <b-input-group-append>
                <b-button size="sm" text="Button" squared variant="primary" @click="getData1">Получить ссылки</b-button>
                <b-button size="sm" text="Button" squared variant="primary" @click="getData2">Опубликовать пост</b-button>
            </b-input-group-append>
        </b-input-group>

        <div>
            <b-form-textarea
                    id="textarea-no-resize"
                    placeholder="Fixed height textarea"
                    rows="3"
                    :value="text"
                    plaintext
            ></b-form-textarea>
        </div>

    </div>
</template>

<script>
    import 'bootstrap/dist/css/bootstrap.css'
    import 'bootstrap-vue/dist/bootstrap-vue.css'

    export default {
        name: 'App',
        data: function () {
            return {
                wallget: [],
                owner_id: '',
                text: '',
            }
        },
        methods: {
            getData1 () {
                this.$jsonp('https://api.vk.com/method/wall.get', { owner_id: this.owner_id, count: 5, access_token: 'f839ff68ac2c4e6b5dae2c15553a0bf2d43116f93c5b8a21fa257c692059429e1099b12403491e8ba6420', v: '5.103' }).then(json => {
                    this.wallget = json.response.items
                    this.text = json.response.items.map(function(text) {
                        return ("https://vk.com/wall-187509252_" + text.id)
                    }).join('\n')


                }).catch(err => {
                    console.log(err)


                })
            },
            getData2 () {
                this.$jsonp('https://api.vk.com/method/wall.post', { owner_id: -62985409, from_group: 1, message: 'hello vue', access_token: 'e86d0afe6d2ed6adf58b33dcf948599199239b1ce37b4b745e9f3c785b6c26f42f18dc4abd509889de07c', v: '5.103' }).then(json => {
                    console.log(json)



                }).catch(err => {
                    console.log(err)


                })
            },
            getData3 () {
                this.$jsonp('https:\\/\\/pu.vk.com\\/c200428\\/ss2009\\/upload.php?act=do_add', { owner_id: -62985409, from_group: 1, message: 'Hello', access_token: 'e86d0afe6d2ed6adf58b33dcf948599199239b1ce37b4b745e9f3c785b6c26f42f18dc4abd509889de07c', v: '5.103' }).then(json => {
                    console.log(json)



                }).catch(err => {
                    console.log(err)


                })
            }


        },

        mounted () {
            // this.getData ()
            console.log(this.owner_id)
        }
    }

</script>