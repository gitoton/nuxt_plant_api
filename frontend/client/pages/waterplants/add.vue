<template>
    <main class="container my-5">
        <div class="row">
            <div class="col-12 text-center my-3">
                <h2 class="mb-3 display-4 text-uppercase">
                    {{ waterplant.name }}
                </h2>
            </div>
            <div class="col-mb-6 mb-4">
                <img 
                    v-if="preview"
                    :src="preview"
                    class="img-fluid"
                    style="width: 400px border-radius: 10px box-shadow: 0 1rem 1rem rgba(0,0,0,0.7)"
                    alt
                >
                <img v-else
                    src="@/static/images/banner.jpg"
                    class="img-fluid"
                    style="width: 400px border-radius: 10px box-shadow: 0 1rem 1rem rgba(0,0,0,0.7)"
                >
            </div>
            <div class="col-mb-4">
                <form @submit.prevent="submitWaterPlant">
                    <div class="form-group">
                        <label for>水草名称</label>
                        <input v-model="waterplant.name" type="text" class="form-control">
                    </div>
                    <div class="form-group">
                        <label for>植える位置</label>
                        <input v-model="waterplant.position" type="text" class="form-control">
                    </div>
                    <div class="form-group">
                        <label for>水草の写真</label>
                        <input @change="onFileChange" type="file" name="file">
                    </div>
                    <div class="row">
                        <div class="col-mb-6">
                            <div class="form-group">
                                <label for>育成難易度</label>
                                <select v-model="waterplant.difficulty" class="form-control">
                                    <option value="Easy">
                                        Easy
                                    </option>
                                    <option value="Medium">
                                        Medium
                                    </option>
                                    <option value="Hard">
                                        Hard
                                    </option>
                                </select>
                            </div>
                        </div>
                        <div class="col-mb-6">
                            <div class="form-group">
                                <label for>二酸化炭素添加量</label>
                                <select v-model="waterplant.addition_amount" class="form-control">
                                    <option value="Low">
                                        Low
                                    </option>
                                    <option value="Middle">
                                        Middle
                                    </option>
                                    <option value="High">
                                        High
                                    </option>
                                </select>
                            </div>
                        </div>
                        <div class="col-mb-6">
                            <div class="form-group">
                                <label for>葉長</label>
                                <small>(mm)</small>
                                <input v-model="waterplant.leaf_length" type="number" class="form-control">
                            </div>
                        </div>
                    </div>
                    <div class="form-group mb-3">
                        <label for>水質</label>
                        <input v-model="waterplant.water_quality" type="text" class="form-control">
                    </div>
                    <button type="submit" class="btn btn-primary">
                        登録
                    </button>
                </form>
            </div>
        </div>
    </main>
</template>
<script>
export default {
    head () {
        return {
            title: '水草追加'
        }
    },
    data () {
        return {
            waterplant: {
                name: '',
                position: '',
                picture: '',
                difficulty: '',
                addition_amount: '',
                leaf_length: '',
                water_quality: '',
            },
            preview: '',
        }
    },
    methods: {
        onFileChange (e) {
            const files = e.target.files || e.dataTransfer.files
            if ( !files.length ) {
                return
            }
            this.waterplant.picture = files[0]
            this.createImage(files[0])
        },
        createImage (file) {
            const reader = new FileReader()
            const vm = this
            reader.onload = (e) => {
                vm.preview = e.target.result
            }
            reader.readAsDataURL(file)
        },
        async submitWaterPlant () {
            const config = { headers: {'content-type': 'multipart/form-data'} }
            const formData = new FormData()
            for (const data in this.waterplant) {
                formData.append(data, this.waterplant[data])
            }
            try {
                const response = await this.$axios.$post(`/waterplants/`, formData, config)
                this.$router.push(`/waterplants/`)
            }catch (e) {
                console.log(e)
            }
        }
    },
}
</script>
<style scoped>
</style>