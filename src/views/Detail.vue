<template>
    <my-page :title="title" backable>
        <div class="empty" v-if="!data.length">
            没有人报餐
        </div>
        <!-- <ul class="log-list">
            <li class="item" v-for="item in data">
                <div class="times">{{ item.user.name }}</div>
            </li>
        </ul> -->
        <ui-article>
            <table>
                <tr>
                    <th>姓名</th>
                    <th>备注</th>
                </tr>
                <tr v-for="item in data">
                    <td>{{ item.user.name }}</td>
                    <td>{{ item.note }}</td>
                </tr>
            </table>
        </ui-article>
    </my-page>
</template>

<script>
    /* eslint-disable */
    export default {
        data () {
            return {
                title: '详情',
                data: [],
                loading: true,
                code: '',
                result: null,
                page: {
                    menu: [
                        // {
                        //     type: 'icon',
                        //     icon: 'help',
                        //     href: 'https://project.yunser.com/products/fd5fcc00fbe011e8a644d75e0db84a23',
                        //     target: '_blank'
                        // }
                    ]
                }
            }
        },
        mounted() {
            this.init()
        },
        methods: {
            init() {
                this.loadData()
            },
            loadData() {
                let {date} = this.$route.query
                this.title = date
                this.$http.get(`/eat/detail?date=${date}`)
                    .then(response => {
                        let data = response.data
                        this.data = data
                    },
                    response => {
                        console.log(response)
                        this.loading = false
                    })
            },
        },
        watch: {
        }
    }
</script>

<style lang="scss" scoped>
    .empty {
        padding: 80px 0;
        text-align: center;
    }
    .count-list {
        max-width: 480px;
        display: flex;
        margin-bottom: 16px;
        .item {
            padding: 16px 0;
            flex-grow: 1;
            margin-right: 16px;
            text-align: center;
            border: 1px solid #ccc;
            border-radius: 4px;
            cursor: pointer;
            &:last-child {
                margin-right: 0;
            }
        }
        .key {
            font-size: 16px;
            color: #666;
        }
        .value {
            font-size: 24px;
        }
        .item-before {
            .value {
                color: #ea4335;
            }
        }
        .item-today {
            .value {
                color: #4285f4;
            }
        }
        .item-after {
            .value {
                color: #34a853;
            }
        }
    }
    .log-list {
        .item {
            display: flex;
        }
        .time {
            margin-right: 16px;
        }
    }
</style>
