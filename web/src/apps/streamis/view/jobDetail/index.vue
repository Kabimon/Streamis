<template>
  <div class="container">
    <div class="navWrap">
      <div @click="jumpToCenter()" class="center">
        <Icon type="ios-home" size="20" />
        <span>{{ $t("message.streamis.routerName.realTimeJobCenter") }}</span>
      </div>
      <div class="slash">/</div>
      <div class="name">{{ name }}</div>
      <div class="version">{{ version }}</div>
      <div class="statusWrap">
        <div class="circle" :style="{ borderColor: status.color, }"></div>
        <p :style="{ color: status.color, }">{{ $t(`message.streamis.jobStatus.${status.name}`) }}</p>
      </div>
      <div class="linkis">
        <Button
          type="primary"
          @click="jumpToLinkis()"
          style="height:24px;background:rgba(22, 155, 213, 1);margin-left: 15px;"
        >
          {{ $t("message.streamis.enterLinkis") }}
        </Button>
      </div>
    </div>
    <Tabs type="card" v-model="choosedModule">
      <TabPane
        name="jobSummary"
        :label="$t('message.streamis.moduleName.jobSummary')"
      >
        <jobSummary />
      </TabPane>
      <TabPane
        name="jobHistory"
        :label="$t('message.streamis.moduleName.jobHistory')"
      >
        <jobHistory />
      </TabPane>
      <TabPane
        name="jobConfig"
        :label="$t('message.streamis.moduleName.jobConfig')"
      >
        <jobConfig />
      </TabPane>
      <TabPane
        name="jobDetail"
        :label="$t('message.streamis.moduleName.jobDetail')"
      >
        <jobDetail />
      </TabPane>
    </Tabs>
  </div>
</template>
<script>
import jobSummary from "@/apps/streamis/module/jobSummary";
import jobHistory from "@/apps/streamis/module/jobHistory";
import jobConfig from "@/apps/streamis/module/jobConfig";
import jobDetail from "@/apps/streamis/module/jobDetail";
import { jobStatuses } from "@/apps/streamis/common/common";
export default {
  components: {
    jobSummary: jobSummary.component,
    jobHistory: jobHistory.component,
    jobDetail: jobDetail.component,
    jobConfig: jobConfig.component
  },
  data() {
    return {
      choosedModule: this.$route.params.module || "jobSummary",
      tabs: ["jobSummary", "jobHistory", "jobConfig", "jobDetail"],
      name: this.$route.params.name,
      version: this.$route.params.version,
      status: this.$route.params.taskStatus
        ? jobStatuses.find(item => item.code === this.$route.params.taskStatus)
        : {}
    };
  },
  mounted() {
    // this.init();
    console.log(this.$route.params);
  },
  methods: {
    resize(height) {
      this.navHeight = height;
    },
    jumpToLinkis() {
      this.$router.push({
        name: "RealTimeJobCenter"
      });
    },
    jumpToCenter() {
      this.$router.push({
        name: "RealTimeJobCenter"
      });
    }
  }
};
</script>
<style lang="scss" scoped>
.container {
  padding: 10px 30px 0;
}
.divider {
  height: 30px;
}
.navWrap {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  font-size: 14px;
  height: 60px;
  .center {
    cursor: pointer;
  }
  .slash {
    padding: 0 10px;
  }
  .name {
    font-weight: 700;
  }
  .version {
    border-radius: 2px;
    padding: 0px 5px;
    background: rgba(22, 155, 213, 1);
    margin-left: 8px;
    color: #fff;
    font-size: 13px;
  }
  .statusWrap {
    display: flex;
    font-size: 12px;
    margin-left: 120px;
    .circle {
      width: 10px;
      height: 10px;
      border: 2px solid #000;
      border-radius: 5px;
      box-sizing: border-box;
      margin-top: 3px;
      margin-right: 3px;
    }
  }
}
</style>
