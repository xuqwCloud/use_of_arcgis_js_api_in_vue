<template>
  <div id="app">
    
  </div>
</template>

<script>
import {loadModules} from 'esri-loader';

export default {
  name: 'app',
  methods: {

      //创建地图
      _createMapView: function() {
            const _self = this;   //定义一个_self防止后续操作中this丢失
            const option = {      //定义一个包含有JS API中js开发包和css样式文件的对象
                url: 'http://localhost/4.14/init.js',
                css: 'http://localhost/4.14/esri/themes/light/main.css',
            };

            //通过loadModules来做衔接
            loadModules(['esri/Map',
            'esri/views/MapView'], option)
                .then(([Map, MapView]) => {
                    
                    //业务代码在此处编写
                    const map = new Map({    //实例化地图
                        basemap: "streets"
                    });

                    const view = new MapView({   //实例化地图视图
                        container: "app",
                        map: map,
                        zoom: 11, 
                        center: [104.072044,30.663776] 
                    });

                    view.ui.components = [];   //清除掉地图左上角默认的缩放图标
                }).catch((err) => {
                    _self.$message('地图创建失败，' + err);
                });
      },
  },
  mounted: function() {
      this._createMapView();
  }
}
</script>

<style>
body {
    margin: 0;   /**主要是去除谷歌浏览器默认的8像素的外边距 */
}
#app {
    position: absolute;   /**使这个div的大小撑满整个屏幕 */
    width: 100%;
    height: 100%;
}
</style>
