<template>
  <div id="rolePowerNewAdd">
    <div id="main" class="fg-table-type" role="main">
      <div id="shopUnit">
        <div class="container">

          <div class="content">
            <el-row :span="24" class="fg-content-title">
              角色权限 - 编辑
            </el-row>
            <el-row :span="24" class="fg-content-detail">

              <el-form :model="FG_role.data" :rules="FG_role.rules" ref="roleForm"
                       label-width="166px"
                       class="demo-form-inline" :inline="true">
                <el-row>

                  <el-form-item label="角色名称 ：" prop="name">
                    <el-input v-model="FG_role.data.name"></el-input>
                    <el-button :plain="true" type="primary" size="" @click="getCheckedKeys('roleForm')"
                               style="margin-left: 10px"><i
                      class="fa fa-save"></i> 保存
                    </el-button>
                    <el-button type="primary" @click="FG_handleResetForm('roleForm')">重置</el-button>
                  </el-form-item>


                  <div class="power-tree">


                    <el-tree
                      :data="FG_power.data"
                      show-checkbox
                      node-key="id"
                      ref="tree"
                      :props="FG_power.defaultProps"
                      :default-checked-keys="FG_power.checkedKeys"
                      default-expand-all>
                    </el-tree>
                    <!-- <div v-for="firstMenu in FG_power.data">
                         <div style="margin-left: 30px">{{firstMenu.name}}</div>
                       <div v-if="firstMenu.children">
                         <div v-for="secondMenu in firstMenu.children">
                           <div v-if="secondMenu.extra">
                             <el-checkbox v-model="secondMenu.extra.checked" style="float: left;margin-left: 40px">{{secondMenu.name}}</el-checkbox>
                              <div v-if="secondMenu.children">
                                  <div v-for="thirdMenu in secondMenu.children">
                                    <div v-if="thirdMenu.extra">
                                      <el-checkbox v-model="thirdMenu.extra.checked" style="float: left;margin-left: 70px">{{thirdMenu.name}}</el-checkbox>
                                    </div>
                                    <div v-else="thirdMenu.extra" >
                                      <div style="margin-left: 90px">{{thirdMenu.name}}</div>
                                    </div>
                                  </div>
                              </div>
                           </div>
                           <div v-else="secondMenu.extra">
                              <div style="margin-left: 60px">{{secondMenu.name}}</div>
                             <div v-if="secondMenu.children">
                               <div v-for="thirdMenu in secondMenu.children">
                                 <div v-if="thirdMenu.extra">
                                   <el-checkbox v-model="thirdMenu.extra.checked" style="float: left;margin-left: 70px">{{thirdMenu.name}}</el-checkbox>
                                 </div>
                                 <div v-else="thirdMenu.extra">
                                   <div style="margin-left: 90px">{{thirdMenu.name}}</div>
                                 </div>
                               </div>
                             </div>
                           </div>

                         </div>
                       </div>

                     </div>-->

                  </div>


                </el-row>

              </el-form>


            </el-row>


          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<style lang="scss">
  #rolePowerNewAdd {

  .el-tree {
    border: none;
  }

  .el-tree-node > .el-tree-node__children > .el-tree-node {
    border: none;
  }

  .power-tree {
    background: white;
    border-radius: 4px;
    width: 1198px;
    margin-left: 57px;
    padding-top: 10px;
    padding-bottom: 20px;
  }

  .el-tree-node {
    border-bottom: 1px dashed #d0d0d0;
  }

  .el-tree-node__content:hover {
    background: none;
  }

  .el-tree-node > .el-tree-node__children > .el-tree-node > .el-tree-node__children > .el-tree-node > .el-tree-node__children > .el-tree-node {
    float: left;
  }

  }

</style>


<script>

  import Helper from '@/assets/admin/js/helper.js'
  import Action from '@/assets/admin/resource/actions.js'
  import Rules from '@/assets/admin/resource/rules.js'
  import {mapMutations} from 'vuex'
  export default {
    data (){
      return {
        merchantList: [],
        FG_role: {
          data: {
            id:'',
            code: '',
            name: '',
            /*   type:1,*/
            isAuthorize: 1
          },
          rules: Rules.System.Role.addForm
        },
        FG_power: {
          data: [],
          checkedKeys: [],
          defaultProps: {
            children: 'children',
            label: 'name'
          }
        }

      }
    },
    created() {
      this.FG_role.data.name = this.$route.query.name
      this.FG_role.data.code = this.$route.query.code
      this.FG_role.data.id = this.$route.query.id
      this.initPrivilege()
    },
    methods: {
      ...mapMutations(['User/INIT_USER_POWER']),
      initPrivilege(){
        this.$http(this.$_.merge({}, Action.System.Role.rolePrivilegeTree, {
          params: {
            roleNo: this.FG_role.data.id
          }
        })).then(response => {
          this.FG_power.data = response.body.children
          for (let i = 0; i < this.FG_power.data.length; i++) {
            if (this.FG_power.data[i].extra.checked) {
              this.FG_power.checkedKeys.push(this.FG_power.data[i].id)
            } else {
              if (this.FG_power.data[i].children) {
                for (let j = 0; j < this.FG_power.data[i].children.length; j++) {
                  if (this.FG_power.data[i].children[j].extra.checked) {
                    this.FG_power.checkedKeys.push(this.FG_power.data[i].children[j].id)
                  } else {
                    if (this.FG_power.data[i].children[j].children) {
                      for (let k = 0; k < this.FG_power.data[i].children[j].children.length; k++) {
                        if (this.FG_power.data[i].children[j].children[k].extra.checked) {
                          this.FG_power.checkedKeys.push(this.FG_power.data[i].children[j].children[k].id)
                        } else {
                          if (this.FG_power.data[i].children[j].children[k].children) {
                            for (let l = 0; l < this.FG_power.data[i].children[j].children[k].children.length; l++) {
                              if (this.FG_power.data[i].children[j].children[k].children[l].extra.checked) {
                                this.FG_power.checkedKeys.push(this.FG_power.data[i].children[j].children[k].children[l].id)
                              }
                            }
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          }

        }, response => {

        })
      },

      getCheckedKeys(formName){
        this.$refs[formName].validate((valid) => {
          if (valid) {
            let menuCodeList = this.$refs.tree.getCheckedKeys().join()

            this.FG_role.data.privilegeCodes = menuCodeList
            this.$http(this.$_.merge({}, Action.System.Role.update, {
              body: this.FG_role.data
            })).then(response => {
              this.$message({
                type: 'success',
                message: '更新成功'
              })
              this.$router.push({path: "/system/role"})
              this.getUserPower()
            }, response => {

            })

          } else {
            return false
          }
        })
      },
      getUserPower(){
        this.$http(this.$_.merge({timeout: 3000,}, Action.Power.list)).then(response => {
          this['User/INIT_USER_POWER'](response.body)
          this.$store.dispatch('User/userPower', response.body);
          //发送结果
          this.$emit('finish', true)
        }, response => {
          this.$emit('finish', false)
        })
      },
      FG_handleResetForm(formName){

        this.initPrivilege()

      },
    },
    mounted() {
    }

  }

</script>
