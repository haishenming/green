<template>
    <div class="home">
        <div class="inputs">
            <a-row type="flex" justify="center">
                <a-col :span="2">
                    <a-input type="number" class="numInput" v-model="nums[0]" placeholder="位置1"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" class="numInput" v-model="nums[1]" placeholder="位置2"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" class="numInput" v-model="nums[2]" placeholder="位置3"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" class="numInput" v-model="nums[3]" placeholder="位置4"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" class="numInput" v-model="nums[4]" placeholder="位置5"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" class="numInput" v-model="nums[5]" placeholder="位置6"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" class="numInput" v-model="nums[6]" placeholder="位置6"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" class="numInput" v-model="nums[7]" placeholder="位置8"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" class="numInput" v-model="nums[8]" placeholder="位置9"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" class="numInput" v-model="nums[9]" placeholder="位置10"/>
                </a-col>
                <a-col :span="2">
                    <a-button type="primary" :span="2" onclick="insert">
                        提交
                    </a-button>
                </a-col>
            </a-row>
        </div>
        <div class="table">
            <a-table :dataSource="insertNums">
                <a-table-column
                        title="位置1"
                        dataIndex="0"
                        key="0"
                >
                </a-table-column>
                <a-table-column
                        title="位置2"
                        dataIndex="0"
                        key="0"
                >
                </a-table-column>
                <a-table-column
                        title="位置3"
                        dataIndex="0"
                        key="0"
                >
                </a-table-column>
                <a-table-column
                        title="位置4"
                        dataIndex="0"
                        key="0"
                >
                </a-table-column>
                <a-table-column
                        title="位置5"
                        dataIndex="0"
                        key="0"
                >
                </a-table-column>
                <a-table-column
                        title="位置6"
                        dataIndex="0"
                        key="0"
                >
                </a-table-column>
                <a-table-column
                        title="位置7"
                        dataIndex="0"
                        key="0"
                >
                </a-table-column>
                <a-table-column
                        title="位置8"
                        dataIndex="0"
                        key="0"
                >
                </a-table-column>
                <a-table-column
                        title="位置9"
                        dataIndex="0"
                        key="0"
                >
                </a-table-column>
                <a-table-column
                        title="位置10"
                        dataIndex="0"
                        key="0"
                >
                </a-table-column>
            </a-table>

        </div>
    </div>
</template>

<script>
	// @ is an alias to /src

	export default {
		name: 'home',
		components: {},
		data() {
			return {
				nums: [],
				insertNums: []
			}
		},
		watch: {
			nums: function (nums) {
				console.log(nums)
				let err = this.checkNums(nums)
				if (err !== "") {
					this.$message.warning(err.message);
					nums[err.i] = null
					return
				}
				if (nums.length === 10) {
					this.insertNums.push(nums).reverse()
				}

			},
		},
		methods: {
			insert: function () {

			},
			checkNums: function (nums) {
				var err = ""
				// 检查是否大于9
				var map = {}
				for (let i in nums) {
					let n = nums[i]
					if (n > 9 || n < 0) {
						err = {message: "数字超出范围", i: i}
					}

					if (map[nums[i]]) {
						err = {message: "数字有重复", i: i}
					}
					map[nums[i]] = true;
				}

				return err
			}
		}
	}
</script>

<style lang="stylus">
    .home
        width 80%
        text-align center
        margin 50px

        .numInput
            max-width 120px

        .table
            width 80%
            margin-top 10px
            margin-left 100px

</style>
