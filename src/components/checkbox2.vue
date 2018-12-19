<template>
 <div>
    <div>
    <template>
<div class="content">
<div class="power">
<h4>权限设置</h4>
<div v-for="(permissionTop, topIndex) in tableData" :key="topIndex" >
<p class="checkGroup" style="width:99%;">
<el-checkbox :indeterminate="permissionTop.indeterminate" :key="topIndex" v-model="permissionTop.mychecked" :label="permissionTop.permissionId" @change="onChangeTop(topIndex, permissionTop.permissionId, $event)">{{permissionTop.permissionName}}</el-checkbox>
</p>
<div style="margin: 15px 0;"></div>
<el-checkbox v-for="permissionSon in permissionTop.childrenList" v-model="permissionSon.mychecked" @change="onChangeSon(topIndex, permissionSon.permissionId, permissionTop.permissionId, $event)" :label="permissionSon.permissionId" :key="permissionSon.permissionId">{{permissionSon.permissionName}}</el-checkbox>
</div>
<el-button class="keep" @click="submitOperatorInfo" >保存</el-button>
</div>
</div>
</template>eateTime" label="创建时间"></el-table-column>
         </el-table>

  </div>

 <el-radio v-model="radio" label="1" class="check1">选择状态1</el-radio>
                   <el-radio v-model="radio" label="2" class="check2">选择状态2</el-radio>
{{radio}}
 </div>
</template>
<script>
export default {
  name:"Checkbox2",
 data(){
        return{
             radio: '1',
            tableData: [
            {
                "childrenList": [
                    {"createTime": 1533707273000,"mychecked": false,"indeterminate": false,"parentPermId": 15,"permissionId": 21,"permissionKey": "orderForm","permissionName": "订单","permissionPath": "","showFlag": "1"},
                    {"createTime": 1533707273000,"mychecked": false,"indeterminate": false,"parentPermId": 15,"permissionId": 22, "permissionKey": "user","permissionName": "用户","permissionPath": "","showFlag": "1"},
                    {"createTime": 1533707273000,"mychecked": false,"indeterminate": false,"parentPermId": 15, "permissionId": 23,"permissionKey": "exportOrderForm","permissionName": "导出订单","permissionPath": "","showFlag": "1"},
                    {"createTime": 1533707273000,"mychecked": false,"indeterminate": false,"parentPermId": 15, "permissionId": 24, "permissionKey": "exportUser", "permissionName": "导出用户","permissionPath": "","showFlag": "1"}
                ],
                "permissionName": "用户服务","mychecked": true,"indeterminate": false,"createTime": 1533707273000,"parentPermId": 0,"permissionId": 15,"permissionKey": "userService","permissionPath": "","showFlag": "1"
            },
            {
                "childrenList": [
                    {"createTime": 1533707273000,"mychecked": false,"indeterminate": false,"parentPermId": 16,"permissionId": 25,"permissionKey": "contentView","permissionName": "内容查看","permissionPath": "","showFlag": "1"},
                    {"createTime": 1533707273000,"mychecked": false,"indeterminate": false,"parentPermId": 16,"permissionId": 26,"permissionKey": "contentAccept","permissionName": "内容采纳","permissionPath": "","showFlag": "1"},
                    {"createTime": 1533707273000,"mychecked": false,"indeterminate": false,"parentPermId": 16,"permissionId": 27,"permissionKey": "distributionCenter","permissionName": "分销中心","permissionPath": "","showFlag": "1"},
                    {"createTime": 1533707273000,"mychecked": false,"indeterminate": false,"parentPermId": 16,"permissionId": 28,"permissionKey": "myMall","permissionName": "我的商城","permissionPath": "","showFlag": "1"}
                ],
                "permissionName": "内容商城","mychecked": true,"indeterminate": false,"createTime": 1533707273000,"parentPermId": 0,"permissionId": 16,"permissionKey": "contentMall","permissionPath": "","showFlag": "1"
            }],
            activeName: 'accountManage',
            people:'',
            phoneNum:'',
            isIndeterminate:true,
        }
    },
mounted(){
        this.refurbishPermissionInfo();//刷新权限信息
    },
mounted(){
        this.refurbishPermissionInfo();//刷新权限信息
    },
    methods: {
        onChangeTop(index, topId, e){//父级change事件
            this.tableData[index].mychecked = e//父级勾选后，子级全部勾选或者取消
            if(e == false) this.tableData[index].indeterminate = false //去掉不确定状态
            var childrenArray = this.tableData[index].childrenList
            if(childrenArray)
                for(var i=0,len=childrenArray.length; i<len; i++)
                    childrenArray[i].mychecked = e
        },
        onChangeSon(topIndex, sonId, topId, e){//子级change事件
            var childrenArray = this.tableData[topIndex].childrenList
            var tickCount = 0, unTickCount = 0, len = childrenArray.length
            for(var i = 0; i < len; i++){
                if(sonId == childrenArray[i].permissionId) childrenArray[i].mychecked = e
                if(childrenArray[i].mychecked == true) tickCount++
                if(childrenArray[i].mychecked == false) unTickCount++
            }
            if(tickCount == len) {//子级全勾选
                this.tableData[topIndex].mychecked = true
                this.tableData[topIndex].indeterminate = false
            } else if(unTickCount == len) {//子级全不勾选
                this.tableData[topIndex].mychecked = false
                this.tableData[topIndex].indeterminate = false
            } else {
                this.tableData[topIndex].mychecked = true
                this.tableData[topIndex].indeterminate = true //添加不确定状态
            }
        },
        refurbishPermissionInfo(){//刷新checkbox
            var userId = 63
            Api.admin.post('/user/findManagerPermissionList?userId='+userId).then(resp => {
                console.log(resp.data)
                if(resp.data.code == 1 && resp.data.data && resp.data.data.length > 0){
                    const checkboxShow = document.getElementById("checkboxShow")
                    const permissionArray = resp.data.data
                    const permissionArrayObj = new Array()
                    for(var i = 0,len = permissionArray.length; i < len; i++){//根权限
                        permissionArrayObj[i] = new Object()
                        permissionArrayObj[i].permissionName = permissionArray[i].permissionName
                        permissionArrayObj[i].permissionId = permissionArray[i].permissionId
                        permissionArrayObj[i].parentPermissionId = permissionArray[i].parentPermId
                        permissionArrayObj[i].mychecked = false
                        permissionArrayObj[i].indeterminate = false
                        if(permissionArray[i].childrenList && permissionArray[i].childrenList.length > 0){//子权限
                            const originalChildrenList = permissionArray[i].childrenList
                            const childrenArray = new Array()
                            for(var j = 0,leng = originalChildrenList.length; j < leng; j++){
                                const childrenObj = new Object()
                                childrenObj.permissionName = originalChildrenList[j].permissionName
                                childrenObj.permissionId = originalChildrenList[j].permissionId
                                childrenObj.parentPermissionId = originalChildrenList[j].parentPermId
                                childrenObj.mychecked = false
                                permissionArrayObj[i].indeterminate = false
                                childrenArray[j] = childrenObj
                            }
                            permissionArrayObj[i].childrenList = childrenArray
                        }
                    }
                    this.tableData = permissionArrayObj
                }
            })
        },
        submitOperatorInfo(){
            var permissionArray = new Array()
            if(this.tableData) {
                for(var i = 0,len = this.tableData.length; i < len; i++){
                    if(this.tableData[i].mychecked == true) permissionArray.push(this.tableData[i].permissionId)
                    if(this.tableData[i].childrenList && this.tableData[i].childrenList.length > 0){
                        var sonPermissionArray = this.tableData[i].childrenList
                        for(var j = 0, leng = sonPermissionArray.length; j < leng; j++)
                            permissionArray.push(sonPermissionArray[j].permissionId)
                    }
                }
            }
            let params = new URLSearchParams();
            params.append('orgUserId', "");//企业ID
            params.append('permissionList[]', permissionArray);//权限ID
            Api.admin.post('/login/addOperators', params).then(resp => {
                if (resp.data.code == 1) {//成功
                    window.location.href = "/ShopManage";//刷新账户管理
                } else return this.$message(resp.data.msg);
            });
        }
    }
}
</script>


