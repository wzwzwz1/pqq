<template>
  <div class="movie-container">
    <div class="header">
      <div class="guass">


      <video autoplay muted loop class="header-video">
        <source src="../../assets/6184263-uhd_4096_2160_25fps.mp4" type="video/mp4">
        Your browser does not support HTML5 video.
      </video>
    </div>
      <div class="header-inner clearfix">
        <div class="movie-info-left">
          <div class="avatar-shadow">
            <el-image class="avatar" :src="movieInfo.moviePoster" fit="cover"/>
          </div>
        </div>
        <div class="movie-info-right">
          <div class="movie-info-msg">
            <h1 class="movie-name">{{movieInfo.movieName}}</h1>
<!--            <h1>&nbsp;|</h1> -->
<!--            <h1>&nbsp;</h1> -->
<!--            <h1>&nbsp;</h1> -->
            <ul>
              <li>{{movieInfo.movieCategoryList}}</li>
<!--              <li>{{movieInfo.movieArea}} / {{movieInfo.movieLength}}分钟</li>-->
              <li>{{movieInfo.movieLength}}分钟</li>
              <li>{{movieInfo.releaseDate}}  开始</li>
            </ul>
          </div>
          <div class="movie-info-btn">
            <el-button class="buy-btn" type="primary" @click="toChooseSession">我要预约</el-button>
          </div>
          <div class="movie-info-score">
            <div class="movie-index box-office-container">
              <span class="movie-index-title">参与人数</span>
              <div style="display: flex;align-items: flex-end;">
                <span class="box-office">{{movieInfo.movieBoxOffice}}</span>
                <span class="unit">人</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="movie-info-detail-container">
      <div class="movie-info-detail clearfix">
        <div class="main-content">
          <div class="crumbs-nav-container">
            <a href="/welcome">票多多</a> &gt; <a href="/movie">活动</a> &gt; {{movieInfo.movieName}}
          </div>
          <el-tabs v-model="activeName">
            <el-tab-pane label="介绍" name="introduction">
              <div class="tab-body">
                <!-- 剧情简介 -->
                <div class="module">
                  <div class="mod-title">
                    <h2>活动简介</h2>
                  </div>
                  <div class="mod-content">
                    <span class="dra">
                      {{movieInfo.movieIntroduction}}
                    </span>
                  </div>
                </div>

                <div v-if="this.$route.params.movieId==='39'" class="module">
                  <div class="mod-title">
                    <h2>精彩视频</h2>
                  </div>
                  <div class="mod-content">
                    <video ref="videoPlayer"
                           :src="videoSource"
                           controls>
                    </video>
                  </div>


                </div>

<!--                &lt;!&ndash; 图集 &ndash;&gt;-->
<!--                <div class="module">-->
<!--                  <div class="mod-title">-->
<!--                    <h2>图集</h2>-->
<!--                    <a class="more" @click="showPictures">全部</a>-->
<!--                  </div>-->
<!--                  <div class="mod-content">-->
<!--                    <div class="pictures-list">-->
<!--                      <div v-if="movieInfo.moviePictures.length === 0">-->
<!--                        暂无图片资源-->
<!--                      </div>-->
<!--&lt;!&ndash;                      <div v-if="this.$route.params.movieId==='39'">&ndash;&gt;-->


<!--&lt;!&ndash;                        <video ref="videoPlayer"&ndash;&gt;-->
<!--&lt;!&ndash;                               :src="videoSource"&ndash;&gt;-->

<!--&lt;!&ndash;                               controls>&ndash;&gt;-->
<!--&lt;!&ndash;                        </video>&ndash;&gt;-->


<!--&lt;!&ndash;                      </div>&ndash;&gt;-->
<!--&lt;!&ndash;                      <div v-else>&ndash;&gt;-->


<!--                      <el-image-->
<!--                          class="default-img"-->
<!--                          :src="movieInfo.moviePictures[0]"-->
<!--                          :preview-src-list="movieInfo.moviePictures"-->
<!--                          v-if="movieInfo.moviePictures.length > 0"-->
<!--                          fit="cover">-->
<!--                      </el-image>-->
<!--                      </div>-->
<!--                      <div class="little-pictures">-->
<!--                        <el-image-->
<!--                            class="default-img"-->
<!--                            v-for="(item,index) in movieInfo.moviePictures.slice(1)"-->
<!--                            :key="index"-->
<!--                            :src="item"-->
<!--                            :preview-src-list="movieInfo.moviePictures"-->
<!--                            fit="cover">-->
<!--                        </el-image>-->
<!--&lt;!&ndash;                      </div>&ndash;&gt;-->
<!--                    </div>-->
<!--                  </div>-->
<!--                </div>-->
<!--              </div>-->
<!--            </el-tab-pane>-->
<!--            <el-tab-pane label="图集" name="pictures">-->
<!--              <div class="tab-body">-->
<!--                <div class="pictures-list">-->
<!--                  <div class="little-pictures">-->
<!--                    <div v-if="movieInfo.moviePictures.length == 0">-->
<!--                      暂无图片资源-->
<!--                    </div>-->
<!--                    <el-image-->
<!--                        fit="cover"-->
<!--                        class="default-img"-->
<!--                        v-for="(item,index) in movieInfo.moviePictures"-->
<!--                        :key="index"-->
<!--                        :src="item"-->
<!--                        :preview-src-list="movieInfo.moviePictures">-->
<!--                    </el-image>-->
<!--                  </div>-->
<!--                </div>-->
<!--              </div>-->
<!--            </el-tab-pane>-->

                <!-- 图集 -->
                <div class="module">
                  <div class="mod-title">
                    <h2>图集</h2>
                    <a class="more" @click="showPictures">全部</a>
                  </div>
                  <div class="mod-content">
                    <div class="pictures-list">
                      <div v-if="movieInfo.moviePictures.length === 0">
                        暂无图片资源
                      </div>
                      <el-image
                        fit="cover"
                        class="default-img"
                        :src="movieInfo.moviePictures[0]"
                        :preview-src-list="movieInfo.moviePictures"
                        v-if="movieInfo.moviePictures.length > 0">
                      </el-image>
                      <div class="little-pictures">
                        <el-image
                          fit="cover"
                          class="default-img"
                          v-for="(item,index) in movieInfo.moviePictures.slice(1)"
                          :key="index"
                          :src="item"
                          :preview-src-list="movieInfo.moviePictures">
                        </el-image>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </el-tab-pane>
            <el-tab-pane label="图集" name="pictures">
              <div class="tab-body">
                <div class="pictures-list">
                  <div class="little-pictures">
                    <div v-if="movieInfo.moviePictures.length == 0">
                      暂无图片资源
                    </div>
                    <el-image
                      fit="cover"
                      class="default-img"
                      v-for="(item,index) in movieInfo.moviePictures"
                      :key="index"
                      :src="item"
                      :preview-src-list="movieInfo.moviePictures">
                    </el-image>
                  </div>
                </div>
              </div>
            </el-tab-pane>


          </el-tabs>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import movieItem from './../../components/movie/movie-item';
import moment from 'moment'
export default {
  name: "MovieInfo",
  components:{
    movieItem
  },
  data() {
    return {
      movieInfo: {
        moviePictures: []
      },
      movieId: this.$route.params.movieId,
      activeName: 'introduction',
      colors: ['#99A9BF', '#F7BA2A', '#FF9900'],
      httpURL: this.global.base,
// 将这里替换为你的视频文件路径
      videoSource: require('../../assets/QQ2024514-01128-HD.mp4'),
      videoWidth: 640,  // 默认宽度
      videoHeight: 480, // 默认高度
      playing: false

    }
  },
  created() {
    this.getMovieInfo()
  },
  methods: {
    async getMovieInfo(){
      const _this = this
      const {data : res} = await axios.get('sysMovie/find/' + this.movieId)
      if(res.code !== 200) return this.$message.error('数据查询失败')
      this.movieInfo = res.data
      this.movieInfo.moviePoster = this.httpURL + JSON.parse(res.data.moviePoster)[0]
      this.movieInfo.moviePictures = JSON.parse(this.movieInfo.moviePictures).map((obj, index) => {
        return this.httpURL + obj
      })
      this.movieInfo.movieCategoryList = this.movieInfo.movieCategoryList.map((obj,index) => {
        return obj.movieCategoryName;
      }).join(" ")
    },
    showPictures(){
      this.activeName = 'pictures'
    },
    //转到购票页面
    toChooseSession(){
      let cinemaId = 1;
      let movieId = 1;
      movieId=this.movieId

      // 使用模板字符串和反引号
      this.$router.push(`/chooseSession/${cinemaId}/${movieId}`);
    },
    togglePlay() {
      const videoElement = this.$refs.videoPlayer;
      if (!this.playing) {
        videoElement.play();
        this.playing = true;
      } else {
        videoElement.pause();
        this.playing = false;
      }
    }
  }
}
</script>

<style scoped>
.movie-container{

}

a{
  text-decoration: none;
  cursor:pointer;
}

.header {
  position: relative; /* 使得视频可以定位相对于这个容器 */
  overflow: hidden; /* 防止视频溢出容器 */
  width: 100%;
  min-width: 1200px;

}

.header-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%; /* 覆盖整个.header区域 */
  object-fit: cover; /* 保持视频的宽高比，覆盖整个容器 */
  z-index: 1; /* 确保视频在内容之后，不干扰内容 */
  filter: blur(5px); /* 应用高斯模糊效果 */
  border-radius: 20px;
}
.header-inner {
  width: 1200px;
  margin-top: 10px;
  margin-left: 20%;
  margin-bottom: 1%;

  position: relative;
  z-index: 2; /* 确保头部内容显示在视频之上 */


}




.clearfix::before, .clearfix::after{
  content: " ";
  display: table;
}

.clearfix::after{
  clear: both;
}

.movie-info-left{
  width: 300px;
  height: 370px;
  float: left;
  position: relative;
  top: 70px;
  overflow: hidden;
  z-index: 9;
}

.avatar-shadow{
  position: relative;
  margin: 0 30px;
  width: 240px;
  height: 330px;
  padding-bottom: 40px;
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAPAAAAAyAgMAAAAfG76+AAAADFBMVEUAAAAAAAAAAAAAAAA16TeWAAAABHRSTlMOAgoGQ0SIeAAAADpJREFUSMdjGAWjYBRgAasoAAwdFACKbB7VPEI076YAUGbzfwrAqOYRormcAjCANodSAEY1j2oexJoBlx1+yE7RXIIAAAAASUVORK5CYII=) no-repeat bottom;
}

.avatar{
  border: 4px solid #fff;
  height: 322px;
  width: 232px;
}

.movie-info-msg{
  position: absolute;
  color: #fff;
  font-size: 14px;
  z-index: 1;
}

.movie-name{
  width: 900px;
  margin-top: 0;
  font-size: 26px;
  line-height: 32px;
  font-weight: 700;
  margin-bottom: 0;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  max-height: 64px;
}

.movie-ename{
  width: 340px;
  font-size: 18px;
  line-height: 1.3;
  margin-bottom: 14px;
}

ul{
  width: 250px;
  list-style: none;
  padding-left: 0;
  margin-bottom: 20px;
}

ul li{
  margin: 12px 0;
  line-height: 100%;
}

.movie-info-btn{
  position: absolute;
  bottom: 20px;
}

.buy-btn{
  margin-top: 10px;
  width: 250px;
  height: 40px;
  font-size: 16px;
  text-align: center;
}

.movie-info-score{
  position: absolute;
  top: 145px;
  left: 342px;
}

.movie-index {
  margin-bottom: 16px;
  color: #fff;
}

.box-office-container{
  display: flex;
  flex-direction: column;
}

.movie-index-title{
  font-size: 12px;
  margin-bottom: 8px;
}

.movie-score-num{
  font-size: 30px;
  color: #ffc600;
  height: 30px;
  line-height: 30px;
  margin-right: 10px;
}

.score-container{
  display: flex;
  flex-direction: column;
  align-items: center;
  font-size: 12px;
}

.box-office{
  font-size: 30px;
}

.unit{
  font-size: 12px;
  padding-left: 1px;
  line-height: 24px;
}

.movie-info-right{
  height: 300px;
  position: relative;
  margin-right: 30px;
  margin-left: 300px;
  margin-top: 70px;
}

.movie-info-detail-container{
  width:800px;
  margin: 0 auto;

}

.movie-info-detail{
  margin-top: 80px;
}

.main-content {
  width: 730px;
  float: left;
  margin-bottom: 20px;
}

.crumbs-nav-container {
  margin-bottom: 25px;
  color: #333;
}

.crumbs-nav-container a{
  color: inherit;
}

.el-tabs >>> .el-tabs__item{
  font-size: 20px;
}

.tab-body{
  margin-top: 40px;
}

.module{
  position: relative;
  margin-bottom: 60px;
}

.mod-title h2{
  display: inline-block;
  margin: 0;
  padding: 0;
  font-weight: 400;
  font-size: 18px;
  color: #333;
  line-height: 18px;
}

.mod-title h2:before {
  float: left;
  content: "";
  display: inline-block;
  width: 4px;
  height: 18px;
  margin-right: 6px;
  background-color: #409EFF;
}

.mod-content{
  margin-top: 20px;
  color: #333;
}

.mod-content .dra{
  font-size: 14px;
  line-height: 26px;
}

.more{
  float: right;
  cursor: pointer;
  font-size: 14px;
  color: #999;
  padding-right: 14px;
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAOCAYAAAASVl2WAAAABmJLR0QA/wD/AP+gvaeTAAAAv0lEQVQY013RTUpDQRAE4G8eghcR8ScgKCIugpJFjuIjqAvBc7jxj0muEnCjiIQQJOImB3GnbnpkfL1qpqqrunpSzvkDPxjhGdq2VarBF3q4wRHknP8RzvCEQzzguCalaHZwiwHecY6XogCf8TjFHh7Rh9Tx3AylIZa4TgWpSBuY4BSrYlFXKsr4bjrTW5HkJJa9SBW4jbtukmKxG5MDLOKqfzEPcB9LzQN8LSdfwxj7eMMlZvV/NFiPzFddEH4Bt5Y1mf3fnDwAAAAASUVORK5CYII=) no-repeat 100%;
}

.portrait{
  margin-bottom: 6px;
  width: 128px;
  height: 170px;
  overflow: hidden;
}

.portrait .default-img{
  width: 128px;
  height: 170px;
}

.pictures-list{
  display: flex;
}

.pictures-list>.el-image:first-child{
  width: 465px;
  height: 258px;
}

.pictures-list .default-img{
  border-style: none;
  cursor: pointer;
  width: 126px;
  height: 126px;
}

.little-pictures{
  width: 262px;
  height: 262px;
  display: flex;
  flex-wrap: wrap;
  margin-left: 10px;
  justify-content: space-between;
}

#pane-pictures .little-pictures{
  width: 100%;
  justify-content: flex-start;
  margin-left: 0;
}

#pane-pictures .default-img{
  margin-top: 10px;
  margin-left: 10px;
}

.user-avatar{
  width: 50px;
  height: 50px;
  margin-right: 20px;
}


.main-header{
  font-size: 16px;
}

.user-name{
  margin-top: 2px;
}
video {
  max-width: 100%;
}
button {
  margin-top: 10px;
  cursor: pointer;
}

</style>
