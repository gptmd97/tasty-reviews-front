<template>
    <div id="map" class="map-container"></div>
</template>

<script>
    export default{
    name: "MapComp", //컴포넌트 이름 지정
    data(){
        return{
            map:null
        };
    },
    
    mounted(){
        if (window.kakao && window.kakao.maps) {
      // 카카오 객체가 있고, 카카오 맵그릴 준비가 되어 있다면 맵 실행
      this.loadMap();
    } else {
      // 없다면 카카오 스크립트 추가 후 맵 실행
      this.loadScript();
    }
    },

    methods: {
        loadScript() {
    const script = document.createElement("script");
    script.src =
    "http://dapi.kakao.com/v2/maps/sdk.js?appkey=25b9c992de80da4abec2d551e2d7761e&autoload=false"; // &autoload=false api를 로드한 후 맵을 그리는 함수가 실행되도록 구현
    script.onload = () => window.kakao.maps.load(this.loadMap); // 스크립트 로드가 끝나면 지도를 실행될 준비가 되어 있다면 지도가 실행되도록 구현

    document.head.appendChild(script); // html>head 안에 스크립트 소스를 추가
},
loadMap() {
    const container = document.getElementById("map"); // 지도를 담을 DOM 영역
    const options = {
    // 지도를 생성할 때 필요한 기본 옵션
    center: new window.kakao.maps.LatLng(33.450701, 126.570667), // 지도의 중심좌표
    level: 3, // 지도의 레벨(확대, 축소 정도)
    };
    this.map = new window.kakao.maps.Map(container, options); // 지도 생성 및 객체 리턴
}

    }

};

</script>

<style scoped>
    .map-container {
        width: 100%;
        height: 100%;
    }

</style>