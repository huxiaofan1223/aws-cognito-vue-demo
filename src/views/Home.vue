<template>
  <div class="home">
    <div class="left">
      <div class="menu-list">
        <div class="menu-item">
          <span>My Profile</span>
        </div>
        <div class="menu-item active">
          <span>Address Book</span>
          <div class="menu-child-list">
            <div class="menu-child-item">
              Upcoming
            </div>
            <div class="menu-child-item">
              Completed
            </div>
            <div class="menu-child-item">
              Canceled
            </div>
          </div>
        </div>
        <div class="menu-item">
          <span>Payments Details</span>
        </div>
        <div class="menu-item">
          <span>Update Password</span>
        </div>
        <div class="menu-item" @click="logout">
          <span>Log out</span>
        </div>
        
      </div>
    </div>
    <div class="right">
      <div class="marginB1rem">Completed Bookings</div>
      <div class="box">
        <div class="between center header">
          <h3>Interior Lightning Service</h3>
          <p class="center">Service description <i class="el-icon-arrow-right"></i></p>
        </div>

        <div class="flex body">
          <div class="body-left">
            <div class="flex">
              <div class="item">
                <label>Contact Name</label>
                <p>Tom Bruce</p>
              </div>
              <div class="item">
                <label>Contact Number:</label>
                <p>0488 888 88</p>
              </div>
            </div>
            <div class="item">
              <label>Service Address:</label>
              <p>Tom Bruce</p>
            </div>
            <div class="item marginB0">
              <label>Service Time:</label>
              <p>Tom Bruce</p>
            </div>
          </div>

          <div class="body-right center justify-center">
           <div>
              <p style="color:#FF990D;">Full Refund</p>
              <label>Amount Paid <i class="el-icon-question"></i></label>
              <p>$50</p>
              <br>
              <label>Amount Paid <i class="el-icon-question"></i></label>
              <p>$50</p>
           </div>
          </div>
        </div>

        <div style="text-align:right;">
          <span>Booking Canceled</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  methods:{
    logout(){
      this.$confirm('确认退出吗?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        localStorage.removeItem('token');
        this.$router.push({path:'/login'})
      })
    }
  }
}
</script>

<style scoped lang="scss">
.home{
  width:800px;
  margin:0 auto;
  display:flex;
  padding:1rem 0;
  .left{
    width:200px;
    .menu-list{
      color:#666666;
      .active{
        color:#FF990D;
      }
      .menu-item{
        padding:5px 20px;
        cursor: pointer;
        transition:all .2s;
        span{
          transition:all .2s;
        }
        &:hover{
          span{
            color:#FF990D;
          }
        }
        .menu-child-list{
          margin-left:10px;
          border-left:1px solid #FF990D;
          .menu-child-item{
            padding:0 10px;
            margin:10px 0;
            color:#666666;
            transition:all .2s;
            &:hover{
              color:#FF990D;
            }
          }
        }
      }
    }
  }
  .right{
    flex:1;
    .box{
      box-shadow: 0 0 5px 5px #ebebeb;
      border-radius:5px !important;
      padding:1rem;
      .header{
        border-bottom:1px solid #ebebeb;
        padding-bottom:1rem;
        p{
          color:#FF990D;
          font-weight:bold;
        }
      }
      .body{
        padding:1rem 0;
        border-bottom:5px solid #ebebeb;
        .body-left{
          border-right:1px solid #ebebeb;
          flex:3;
          .item{
            margin-bottom:1rem;
            margin-right:2rem;
            label{
              color:#999999;
            }
          }
        }
        .body-right{
          flex:1;
          label{
            color:#777777;
            i{
              font-size:13px;
            }
          }
        }
      }
    }
    .marginB1rem{
      margin-bottom:1rem;
    }
    .marginB0{
      margin-bottom: 0!important;
    }
  }
}
</style>
