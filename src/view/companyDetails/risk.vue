<template>
  <div>
    <div class="risk" v-show="showFlag.indexOf('2-1')>-1">
      <div class="titles"></div>
      <span class="weni">判决文书</span>
    </div>
    <div v-show="showFlag.indexOf('2-1')>-1">
      <el-table :data="tableData" class="tableList" border>
        <el-table-column type="index" label="序号" width="60"></el-table-column>
        <el-table-column prop="date" label="判决时间" width="100"></el-table-column>
        <el-table-column prop="type" label="案件类型" width="80"></el-table-column>
        <el-table-column label="案件结果">
          <template slot-scope="scope">
            <span
              @click="getDetail(scope.row.id)"
              style="color:#557bf7;cursor: pointer;"
            >{{scope.row.title}}</span>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <div class="riskn" v-show="showFlag.indexOf('2-2')>-1">
      <div class="titlest"></div>
      <span class="wenik">法院公告</span>
    </div>
    <div v-show="showFlag.indexOf('2-2')>-1">
      <el-table :data="hookList" class="tableList" border>
        <el-table-column type="index" label="序号" width="60"></el-table-column>
        <el-table-column prop="date" label="发布时间" width="100"></el-table-column>
        <el-table-column prop="type" label="公告类型" width="130"></el-table-column>
        <el-table-column prop="content" label="公告内容"></el-table-column>
      </el-table>
    </div>
    <div class="BrokenPromises" v-show="showFlag.indexOf('2-3')>-1">
      <div class="BrokenPromisesst"></div>
      <span class="BrokenPromisesk">失信信息</span>
    </div>
    <div v-show="showFlag.indexOf('2-3')>-1">
      <el-table :data="BrokenPromises" class="BrokenPromisesList" border>
        <el-table-column type="index" label="序号" width="60"></el-table-column>
        <el-table-column prop="date" label="立案时间" width="100"></el-table-column>
        <el-table-column prop="case_number" label="案号" width="180"></el-table-column>
        <el-table-column prop="doc_number" label="执行依据文号"></el-table-column>
        <el-table-column prop="court" label="执行法院" width="180"></el-table-column>
        <el-table-column prop="execution_status" label="被执行人履行情况"></el-table-column>
      </el-table>
    </div>
    <div class="Business" v-show="showFlag.indexOf('2-4')>-1">
      <div class="Businessst"></div>
      <span class="Businessk">经营异常</span>
    </div>
    <div v-show="showFlag.indexOf('2-4')>-1">
      <el-table :data="Business" class="tableList" border>
        <el-table-column type="index" label="序号" width="60"></el-table-column>
        <el-table-column prop="in_date" label="列入日期" width="100"></el-table-column>
        <el-table-column prop="department" label="做出决定机关" width="80"></el-table-column>
        <el-table-column prop="in_reason" label="列入经营异常名录原因"></el-table-column>
        <el-table-column prop="out_reason" label="移出日期"></el-table-column>
        <el-table-column prop="out_reason" label="移出经营异常名录原因"></el-table-column>
      </el-table>
    </div>
    <div class="administrativePunishment" v-show="showFlag.indexOf('2-5')>-1">
      <div class="administrativePunishmentst"></div>
      <span class="administrativePunishmentk">行政处罚</span>
    </div>
    <div v-show="showFlag.indexOf('2-5')>-1">
      <el-table :data="administrativePunishment" class="tableList" border>
        <el-table-column type="index" label="序号" width="60"></el-table-column>
        <el-table-column prop="date" label="处罚日期" width="100"></el-table-column>
        <el-table-column prop="number" label="处决文书号" width="180"></el-table-column>
        <el-table-column prop="content" label="处罚内容"></el-table-column>
        <el-table-column prop="department" label="处罚机关"></el-table-column>
        <el-table-column label="详情" width="80">
          <template slot-scope="scope">
            <span style="color:#557bf7;cursor: pointer;" @click="detail(scope.row)">详情</span>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <div class="EquityPledge" v-show="showFlag.indexOf('2-6')>-1">
      <div class="EquityPledgest"></div>
      <span class="EquityPledgek">股权出质</span>
    </div>
    <div v-show="showFlag.indexOf('2-6')>-1">
      <el-table :data="EquityPledge" class="tableList" border>
        <el-table-column type="index" label="序号" width="60"></el-table-column>
        <el-table-column prop="date" label="登记日期" width="100"></el-table-column>
        <el-table-column prop="number" label="登记编号" width="200"></el-table-column>
        <el-table-column prop="pledgor" label="出质人"></el-table-column>
        <el-table-column prop="pawnee" label="质权人"></el-table-column>
        <el-table-column prop="status" label="状态" width="80"></el-table-column>
        <el-table-column label="详情" width="80">
          <template slot-scope="scope">
            <span style="color:#557bf7;cursor: pointer;" @click="equityPledgedetail(scope.row)">详情</span>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <div class="freeze" v-show="showFlag.indexOf('2-7')>-1">
      <div class="freezest"></div>
      <span class="freezek">股权冻结</span>
    </div>
    <div v-show="showFlag.indexOf('2-7')>-1">
      <el-table :data="freeze" class="tableList" border>
        <el-table-column type="index" label="序号" width="60"></el-table-column>
        <el-table-column prop="be_executed_person" label="被执行人" width="160"></el-table-column>
        <el-table-column prop="amount" label="股权数额" width="80"></el-table-column>
        <el-table-column prop="number" label="执行通知书文号"></el-table-column>
        <el-table-column prop="detail.public_date" label="起止日期">
          <template slot-scope="scope">
              <span>{{ scope.row.detail.freeze_start_date }} - {{ scope.row.detail.freeze_end_date }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="status" label="类型/状态"></el-table-column>
        <el-table-column label="详情" width="80">
          <template slot-scope="scope">
            <span style="color:#557bf7;cursor: pointer;" @click="freezedetail(scope.row)">详情</span>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <div class="FilInformation" v-show="showFlag.indexOf('2-8')>-1">
      <div class="FilInformationst"></div>
      <span class="FilInformationk">立案信息</span>
    </div>
    <div v-show="showFlag.indexOf('2-8')>-1">
      <el-table :data="FilInformation" class="FilInformationList" border>
        <el-table-column type="index" label="序号" width="60"></el-table-column>
        <el-table-column prop="case_No" label="案号"></el-table-column>
        <el-table-column prop="hearing_date" label="开庭时间" width="120"></el-table-column>
        <el-table-column prop="related_items[0].role" label="身份" width="80"></el-table-column>
        <el-table-column prop="name" label="详情" width="80">
          <template slot-scope="scope">
            <span style="color:#557bf7;cursor: pointer;" @click="detail2(scope.row)">详情</span>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <div class="hearingAnnouncement" v-show="showFlag.indexOf('2-9')>-1">
      <div class="hearingAnnouncementst"></div>
      <span class="hearingAnnouncementK">开庭公告</span>
    </div>
    <div v-show="showFlag.indexOf('2-9')>-1">
      <el-table :data="hearingAnnouncement" class="hearingAnnouncementList" border>
        <el-table-column type="index" label="序号" width="50"></el-table-column>
        <el-table-column prop="hearing_date" label="开庭日期" width="160"></el-table-column>
        <el-table-column prop="case_reason" label="案由" width="140"></el-table-column>
        <el-table-column prop="plaintiff" label="原告/上诉人" width="160"></el-table-column>
        <el-table-column prop="defendant" label="被告/被上诉人" width="160"></el-table-column>
        <el-table-column prop label="详情">
          <template slot-scope="scope">
            <span style="color:#557bf7;cursor: pointer;" @click="detail3(scope.row)">详情</span>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <el-dialog :title="details.title" :visible.sync="dialogVisible" width="50%" center>
      <p class="content" v-html="details.content"></p>
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>
    <el-dialog title="行政处罚详情" :visible.sync="dialogVisible1" width="40%" center>
      <table>
        <tr>
          <td class=left>决定文书号</td>
          <td class="right">{{item.number}}</td>
        </tr>
         <tr>
          <td class=left>处罚类型</td>
          <td class="right">{{item.illegal_type}}</td>
        </tr>
         <tr>
          <td class=left>处罚机关</td>
          <td class="right">{{item.department}}</td>
        </tr>
         <tr>
          <td class=left>处罚日期</td>
          <td class="right">{{item.date}}</td>
        </tr>
         <tr>
          <td class=left>公示日期</td>
          <td class="right">{{item.publish_date}}</td>
        </tr>
         <tr>
          <td class=left>处罚内容</td>
          <td class="right">{{item.content}}</td>
        </tr>
         <!-- <tr>
          <td class=left>处罚依据</td>
          <td class="right">{{item.number}}</td>
        </tr> -->
      </table>
      
    </el-dialog>
    <el-dialog title="立案信息详情" :visible.sync="dialogVisible2" width="40%" center>
      <table>
        <tr>
          <td class=left>案号</td>
          <td class="right">{{item2.case_no}}</td>
        </tr>
         <tr>
          <td class=left>承办法官</td>
          <td class="right">{{item2.agent}}</td>
        </tr>
         <tr>
          <td class=left>法官助理</td>
          <td class="right">{{item2.assistant}}</td>
        </tr>
         <tr>
          <td class=left>立案时间</td>
          <td class="right">{{item2.start_date}}</td>
        </tr>
         <tr>
          <td class=left>开庭时间</td>
          <td class="right">{{item2.hearing_date}}</td>
        </tr>
         <tr>
          <td class=left>结束时间</td>
          <td class="right">{{item2.end_date}}</td>
        </tr>
          <tr>
          <td class=left>案件状态</td>
          <td class="right">{{item2.case_status}}</td>
        </tr>
        <tr>
          <td class=left>被告</td>
          <td class="right">{{item2.related_items[0].items[0].name}}</td>
        </tr>
        <tr>
          <td class=left>原告</td>
          <td class="right">{{item2.related_items[1].items[0].name}}</td>
        </tr>
      </table>

    </el-dialog>
    <el-dialog title="开庭公告详情" :visible.sync="dialogVisible3" width="40%" center>
      <table>
        <tr>
          <td class=left>开庭日期</td>
          <td class="right">{{item3.hearing_date}}</td>
        </tr>
         <tr>
          <td class=left>案号</td>
          <td class="right">{{item3.case_no}}</td>
        </tr>
         <tr>
          <td class=left>案由</td>
          <td class="right">{{item3.case_reason}}</td>
        </tr>
         <tr>
          <td class=left>承办部门</td>
          <td class="right">{{item3.court}}</td>
        </tr>
         <tr>
          <td class=left>审判长/主审人</td>
          <td class="right">{{item3.judge}}</td>
        </tr>
         <tr>
          <td class=left>原告/上诉人</td>
          <td class="right">{{item3.plaintiff}}</td>
        </tr>
         <tr>
          <td class=left>被告/上诉人</td>
          <td class="right">{{item3.defendant}}</td>
        </tr>
         <!-- <tr>
          <td class=left>处罚依据</td>
          <td class="right">{{item3.number}}</td>
        </tr> -->
      </table>
    </el-dialog>
     <el-dialog title="股权出质详情" :visible.sync="EquityPledgeDialog" width="50%" center>
      <table>
        <table>
        <tr>
          <td class="left">登记编号</td>
          <td class="right">{{EquityPledgeItem.number}}</td>
          <td class="left">状态</td>
          <td class="right">{{EquityPledgeItem.status}}</td>
        </tr>
        <tr>
          <td class="left">出质人</td>
          <td class="right">{{EquityPledgeItem.pledgor}}</td>
          <td class="left">出质股权数</td>
          <td class="right">{{EquityPledgeItem.pledgor_amount}}</td>
        </tr>
        <tr>
          <td class="left">出质人证件号码</td>
          <td class="right">{{EquityPledgeItem.pledgor_identify_no}}</td>
          <td class="left">质权人</td>
          <td class="right">{{EquityPledgeItem.pawnee}}</td>
        </tr>
        <tr>
          <td class="left">质权人证件号码</td>
          <td class="right">{{EquityPledgeItem.pawnee_identify_no}}</td>
          <td class="left">登记日期</td>
          <td class="right">{{EquityPledgeItem.date}}</td>
        </tr>
        <tr>
          <td class="left">备注</td>
          <td colspan="3" class="right">{{EquityPledgeItem.remark}}</td>
        </tr>
      </table>
      </table>
      
    </el-dialog>
    <el-dialog title="股权冻结详情" :visible.sync="freezeDialog" width="50%" center>
      <br><p>冻结情况</p><br>
      <table>
        <tr>
          <td class="left">执行法院</td>
          <td class="right">{{freezeItem.detail.execute_court}}</td>
          <td class="left">执行事项</td>
          <td class="right">{{freezeItem.detail.assist_item}}</td>
        </tr>
        <tr>
          <td class="left">执行裁定文书</td>
          <td class="right">{{freezeItem.detail.notice_no}}</td>
          <td class="left">执行通知文书号</td>
          <td class="right">{{freezeItem.detail.adjudicate_no}}</td>
        </tr>
        <tr>
          <td class="left">被执行人</td>
          <td class="right">{{freezeItem.detail.assist_name}}</td>
          <td class="left">被执行人持有股权丶其它投资权益的数额</td>
          <td class="right">{{freezeItem.detail.freeze_amount}}</td>
        </tr>
        <tr>
          <td class="left">被执行人证件种类</td>
          <td class="right">{{freezeItem.detail.assist_ident_type}}</td>
          <td class="left">被执行人证件号码</td>
          <td class="right">{{freezeItem.detail.assist_ident_no}}</td>
        </tr>
        <tr>
          <td class="left">冻结期限自</td>
          <td class="right">{{freezeItem.detail.freeze_start_date}}</td>
          <td class="left">冻结期限至</td>
          <td class="right">{{freezeItem.detail.freeze_end_date}}</td>
        </tr>
        <tr>
          <td class="left">冻结期限</td>
          <td class="right">{{freezeItem.detail.freeze_year_month}}</td>
          <td class="left">公示日期</td>
          <td class="right">{{freezeItem.detail.public_date}}</td>
        </tr>
      </table>
      <br><p>解冻情况</p><br>
      <table v-if="freezeItem.un_freeze_details.length>0">
        <tr>
          <td class="left">执行裁定文书</td>
          <td class="right">{{freezeItem.un_freeze_details[0].notice_no}}</td>
          <td class="left">执行通知文书号</td>
          <td class="right">{{freezeItem.un_freeze_details[0].adjudicate_no}}</td>
        </tr>
        <tr>
          <td class="left">被执行人</td>
          <td class="right">{{freezeItem.un_freeze_details[0].assist_name}}</td>
          <td class="left">被执行人持有股权丶其它投资权益的数额</td>
          <td class="right">{{freezeItem.un_freeze_details[0].freeze_amount}}</td>
        </tr>
        <tr>
          <td class="left">被执行人证件种类</td>
          <td class="right">{{freezeItem.un_freeze_details[0].assist_ident_type}}</td>
          <td class="left">被执行人证件号码</td>
          <td class="right">{{freezeItem.un_freeze_details[0].assist_ident_no}}</td>
        </tr>
        <tr>
          <td class="left">冻结期限</td>
          <td class="right">{{freezeItem.un_freeze_details[0].freeze_year_month}}</td>
          <td class="left">公示日期</td>
          <td class="right">{{freezeItem.un_freeze_details[0].public_date}}</td>
        </tr>
      </table>
      <p v-else>&nbsp;&nbsp;&nbsp;暂无信息</p>
      <br><p>失效情况</p><br>
      <table style="height:50px">
        <tr>
          <td class="left">失效时间</td>
          <td class="right">{{freezeItem.lose_efficacy.date}}</td>
          <td class="left">失效原因</td>
          <td class="right">{{freezeItem.lose_efficacy.reason}}</td>
        </tr>
      </table>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [],
      hookList: [],
      BrokenPromises: [], //失信name enterprise/getSeriousIllegalByName
      Business: [], //经营id v2/abnormal/getAbnormalListByName
      administrativePunishment: [], //行政处罚keyword v2/adminPunish/getAdminPunishByName
      EquityPledge: [], //股权出质name v2/equityPledge/getEquityQualitiesByName
      freeze: [], //冻结name v2/judicialFreeze/getJudicialFreezeByName
      FilInformation: [], //立案信息id /case/getCaseListById
      hearingAnnouncement: [], //开庭公告id courtnotice/getCourtNoticeByName
      details: {},
      dialogVisible:false,
      item:{},
      item2:{
        related_items:[
          {
            items:[
              {name:'1'}
            ]
          },
          {
            items:[
              {name:'1'}
            ]
          }
        ]
      },
      item3:{},
      dialogVisible1:false,
      dialogVisible2:false,
      dialogVisible3:false,
      EquityPledgeItem:{},
      EquityPledgeDialog: false,
      freezeItem: {
        detail:{
          execute_court:"",
          assist_item:"",
          notice_no:"",
          adjudicate_no:"",
          assist_name:"",
          freeze_amount:"",
          assist_ident_type:"",
          assist_ident_no:"",
          freeze_start_date:"",
          freeze_end_date:"",
          freeze_year_month:"",
          public_date:""
        },
        un_freeze_details:[{
          execute_court:"",
          assist_item:"",
          notice_no:"",
          adjudicate_no:"",
          assist_name:"",
          freeze_amount:"",
          assist_ident_type:"",
          assist_ident_no:"",
          freeze_start_date:"",
          freeze_end_date:"",
          freeze_year_month:"",
          public_date:""
        }],
        lose_efficacy:{
          date:"",
          reason:""
        }
      },
      freezeDialog:false
    };
  },
  props: {
    showFlag: {
      default() {
        return ["2-1", "2-2", "2-3", "2-4", "2-5", "2-6", "2-7", "2-8", "2-9"];
      }
    }
  },
  methods: {
    freezedetail(item){
      console.log(item);
      this.freezeDialog = true
      this.freezeItem = item
    },
    equityPledgedetail(item){
      this.EquityPledgeDialog = true
      this.EquityPledgeItem = item
    },
    detail(item) {
      this.dialogVisible1 = true
      this.item = item
    },
    detail2(item) {
      this.dialogVisible2 = true
      this.$post("/company/invoke", {
        url: "/case/getCaseDetailById",
        id:item.case_id
      }).then(res => {
        console.log('立案详情',res);
        this.item2 = res.data
      });

    },
    detail3(item) {
      this.dialogVisible3 = true
      this.item3 = item
    },
    getDetail(id) {
      this.$post("/company/invoke", {
        url: "/lawsuit/getLawsuitDetail",
        id
      }).then(res => {
        this.dialogVisible = true
        console.log(res);
        this.details = res.data
      });
    },
    detaList() {
      var riskId = sessionStorage.getItem("enterpriseId");
      this.$post("/company/invoke", {
        url: "/lawsuit/getLawsuitListById",
        id: riskId
      })
        .then(data => {
          console.log("判决文书", data);
          this.tableData = data.data.items;
        })
        .catch(error => {
          console.log(1);
        });
    },
    detaList2() {
      var riskId = sessionStorage.getItem("enterpriseId");
      this.$post("/company/invoke", {
        url: "/notice/getNoticeListById",
        id: riskId
      })
        .then(data => {
          console.log("法院公告", data);
          this.hookList = data.data.items;
        })
        .catch(error => {
          console.log(1);
        });
    },
    getBrokenPromises() {
      this.$post("/company/invoke", {
        url: "/execution/getExecutionListById",
        id: sessionStorage.getItem("enterpriseId")
      })
        .then(data => {
          console.log("失信信息",data);
          this.BrokenPromises = data.data.items;
        })
        .catch(error => {
          console.log(1);
        });
    },
    getBusiness() {
      var name = sessionStorage.getItem("SHANGJIAOSUOCOMPANYNAME");
      this.$post("/company/invoke", {
        url: "/v2/abnormal/getAbnormalListByName",
        name: name
      })
        .then(data => {
          console.log(data);
          this.Business = data.data.items;
        })
        .catch(error => {
          console.log(1);
        });
    },
    getadministrativePunishment() {
      var administrativePunishmentkeyword = sessionStorage.getItem(
        "SHANGJIAOSUOCOMPANYNAME"
      );
      this.$post("/company/invoke", {
        url: "/v2/adminPunish/getAdminPunishByName",
        keyword: administrativePunishmentkeyword
      })
        .then(data => {
          console.log("行政处罚",data);
          this.administrativePunishment = data.data.items;
        })
        .catch(error => {
          console.log(1);
        });
    },
    getEquityPledge() {
      var EquityPledgeName = sessionStorage.getItem("SHANGJIAOSUOCOMPANYNAME");
      this.$post("/company/invoke", {
        url: "/v2/equityPledge/getEquityQualitiesByName",
        name: EquityPledgeName
      })
        .then(data => {
          console.log("股权出质",data);
          this.EquityPledge = data.data.items;
        })
        .catch(error => {
          console.log(1);
        });
    },
    getfreeze() {
      var freezeName = sessionStorage.getItem("SHANGJIAOSUOCOMPANYNAME");
      this.$post("/company/invoke", {
        url: "/v2/judicialFreeze/getJudicialFreezeByName",
        name: freezeName
      })
        .then(data => {
          console.log("股权冻结", data);
          this.freeze = data.data.items;
        })
        .catch(error => {
          console.log(1);
        });
    },
    getFilInformation() {
      var FilInformationId = sessionStorage.getItem("enterpriseId");
      this.$post("/company/invoke", {
        url: "/case/getCaseListById",
        id: FilInformationId
      })
        .then(data => {
          console.log("立案信息", data);
          this.FilInformation = data.data.items;
        })
        .catch(error => {
          console.log(1);
        });
    },
    gethearingAnnouncement() {
      var freezeName = sessionStorage.getItem("SHANGJIAOSUOCOMPANYNAME");
      this.$post("/company/invoke", {
        url: "/courtnotice/getCourtNoticeByName",
        name: freezeName
      })
        .then(data => {
          console.log("开庭公告", data);
          this.hearingAnnouncement = data.data.items;
        })
        .catch(error => {
          console.log(1);
        });
    }
  },
  created() {
    this.detaList();
    this.detaList2();
    this.getBrokenPromises();
    this.getBusiness();
    this.getadministrativePunishment();
    this.getEquityPledge();
    this.getfreeze();
    this.getFilInformation();
    this.gethearingAnnouncement();
  }
};
</script>

<style scoped>
table{
  width: 100%;
  height: 200px;
}
td{
  border: 1px solid #dedede;
}
.left{
  color: #c1c6d0;
  width: 105px;
  height: 32px;
  background: #fcfcfc;
  padding-left: 10px;
}
.right{
  padding-left: 10px;
  color: #919398;
}
.risk {
  margin-left: 26px;
  margin-top: 15px;
}
.titles {
  display: inline-block;
  width: 5px;
  margin-right: -1px;
  height: 14px;
  background-color: #557bf7;
  transform: translateY(1px);
}
.tableList {
  margin-left: 26px;
  margin-top: 10px;
  width: 90%;
  background: #fcfcff;
}
.rowClass {
  font-weight: bold;
  color: #838895;
}
.waring-row {
  background: #fcfcff;
}
.riskn {
  margin-left: 26px;
  margin-top: 20px;
}
.wenik {
  font-weight: bold;
  color: #838895;
}
.weni {
  font-weight: bold;
  color: #838895;
}
.titlest {
  display: inline-block;
  width: 5px;
  margin-right: -1px;
  height: 14px;
  background-color: #557bf7;
  transform: translateY(1px);
}
.tableList {
  margin-left: 26px;
  margin-top: 10px;
  width: 90%;
  background: #fcfcff;
}
.rowClass {
  font-weight: bold;
  color: #838895;
}
.waring-row {
  background: #fcfcff;
}
.block {
  width: 100px;
  height: 100px;
  margin-left: 60%;
  margin-top: 16px;
}
.BrokenPromises {
  margin-left: 26px;
  margin-top: 15px;
}
.BrokenPromisesst {
  display: inline-block;
  width: 5px;
  margin-right: -1px;
  height: 14px;
  background-color: #557bf7;
  transform: translateY(1px);
}
.BrokenPromisesk {
  font-weight: bold;
  color: #838895;
}
.BrokenPromisesList {
  margin-left: 26px;
  margin-top: 10px;
  width: 90%;
  background: #fcfcff;
}

.Business {
  margin-left: 26px;
  margin-top: 15px;
}
.Businessst {
  display: inline-block;
  width: 5px;
  margin-right: -1px;
  height: 14px;
  background-color: #557bf7;
  transform: translateY(1px);
}
.Businessk {
  font-weight: bold;
  color: #838895;
}
.BusinessList {
  margin-left: 26px;
  margin-top: 10px;
  width: 90%;
  background: #fcfcff;
}
.administrativePunishment {
  margin-left: 26px;
  margin-top: 15px;
}
.administrativePunishmentst {
  display: inline-block;
  width: 5px;
  margin-right: -1px;
  height: 14px;
  background-color: #557bf7;
  transform: translateY(1px);
}
.administrativePunishmentk {
  font-weight: bold;
  color: #838895;
}
.administrativePunishmentList {
  margin-left: 26px;
  margin-top: 10px;
  width: 90%;
  background: #fcfcff;
}
.EquityPledge {
  margin-left: 26px;
  margin-top: 15px;
}
.EquityPledgest {
  display: inline-block;
  width: 5px;
  margin-right: -1px;
  height: 14px;
  background-color: #557bf7;
  transform: translateY(1px);
}
.EquityPledgek {
  font-weight: bold;
  color: #838895;
}
.EquityPledgeList {
  margin-left: 26px;
  margin-top: 10px;
  width: 90%;
  background: #fcfcff;
}
.freeze {
  margin-left: 26px;
  margin-top: 15px;
}
.freezest {
  display: inline-block;
  width: 5px;
  margin-right: -1px;
  height: 14px;
  background-color: #557bf7;
  transform: translateY(1px);
}
.freezek {
  font-weight: bold;
  color: #838895;
}
.freezeList {
  margin-left: 26px;
  margin-top: 10px;
  width: 90%;
  background: #fcfcff;
}
.FilInformation {
  margin-left: 26px;
  margin-top: 15px;
}
.FilInformationst {
  display: inline-block;
  width: 5px;
  margin-right: -1px;
  height: 14px;
  background-color: #557bf7;
  transform: translateY(1px);
}
.FilInformationk {
  font-weight: bold;
  color: #838895;
}
.FilInformationList {
  margin-left: 26px;
  margin-top: 10px;
  width: 90%;
  background: #fcfcff;
}
.hearingAnnouncement {
  margin-left: 26px;
  margin-top: 15px;
}
.hearingAnnouncementst {
  display: inline-block;
  width: 5px;
  margin-right: -1px;
  height: 14px;
  background-color: #557bf7;
  transform: translateY(1px);
}
.hearingAnnouncementK {
  font-weight: bold;
  color: #838895;
}
.hearingAnnouncementList {
  margin-left: 26px;
  margin-top: 10px;
  width: 90%;
  background: #fcfcff;
}
</style>
