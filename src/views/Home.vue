<template>
    <div class="home">
        <div class="inputs">
            <a-row style="margin: 20px" type="flex" justify="center">
                <a-col :span="2">
                    <a-select defaultValue="15" style="width: 120px" v-model="maxNumsLen">
                        <a-select-option v-for="m in maxSelect" :value="m">{{ m }}</a-select-option>
                    </a-select>
                </a-col>
            </a-row>
            <a-row type="flex" justify="center">
                <a-col :span="2">
                    <a-input type="number" ref="i0" class="numInput" v-model="nums[0]" placeholder="位置1"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" ref="i1" class="numInput" v-model="nums[1]" placeholder="位置2"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" ref="i2" class="numInput" v-model="nums[2]" placeholder="位置3"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" ref="i3" class="numInput" v-model="nums[3]" placeholder="位置4"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" ref="i4" class="numInput" v-model="nums[4]" placeholder="位置5"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" ref="i5" class="numInput" v-model="nums[5]" placeholder="位置6"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" ref="i6" class="numInput" v-model="nums[6]" placeholder="位置6"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" ref="i7" class="numInput" v-model="nums[7]" placeholder="位置8"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" ref="i8" class="numInput" v-model="nums[8]" placeholder="位置9"/>
                </a-col>
                <a-col :span="2">
                    <a-input type="number" @keyup.enter="insert" ref="i9" class="numInput" v-model="nums[9]" placeholder="位置10"/>
                </a-col>
            </a-row>
        </div>
        <div class="table">
            <table class="table">
                <thead>
                <tr>
                    <th>位置1</th>
                    <th>位置2</th>
                    <th>位置3</th>
                    <th>位置4</th>
                    <th>位置5</th>
                    <th>位置6</th>
                    <th>位置7</th>
                    <th>位置8</th>
                    <th>位置9</th>
                    <th>位置10</th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="ns in insertNums">
                    <td v-for="n in ns">
                        <div v-if="n.isGreen" style="color:white; background-color: green">{{n.n}}</div>
                        <div v-else style="color:white; background-color: red">{{n.n}}</div>
                    </td>
                </tr>
                </tbody>
            </table>
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
				insertNums: [],
				maxNumsLen: "15",
                maxSelect: [
                	1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20
                ],
                useableNums: [
                	1,2,3,4,5,6,7,8,9,0
                ]
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
				} else {
					let fi = nums.length.toString()
                    this.$refs["i" + fi].focus()
				}



			},
		},
		methods: {
			insert: function () {
				let nums = this.nums
				let inum = []
				for (let i in nums) {
					let type = 1
					if (i < 5) {
						type = 0
					}
					inum[i] = {n: nums[i], type: type, isGreen: true}
				}
				if (this.insertNums.length === 0) {
					this.insertNums[0] = inum
				} else {
					let lastInum = this.insertNums[0]
					for (let i in inum) {
						for (let j in lastInum) {
							if (lastInum[j].n === inum[i].n) {
								console.log(i, j)
                                console.log(lastInum[j].n, inum[i].n)
                                // 修改位置的颜色，而不是号码的颜色
								inum[j].isGreen = lastInum[j].type === inum[i].type
							}
						}
					}
					console.log("inum", inum)
					console.log("lastInum", lastInum)
					this.insertNums.unshift(inum)
					// this.insertNums.reverse()
				}

				if (this.insertNums.length > this.maxNumsLen) {
					this.insertNums.pop()
                }

				this.nums = []
				this.$refs["i1"].focus()
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
			},
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
            width 92%
            margin-top 10px
            margin-left 50px
            td
                border-left: 20px solid white;

</style>
