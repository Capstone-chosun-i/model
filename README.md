# 20174335 김성욱
  
## _CAPSTONE DESIGN 1_


주제 : 기온별 패션 추천 웹사이트

<img width="501" alt="KakaoTalk_20220616_160145216" src="https://user-images.githubusercontent.com/96335258/174012246-9188539f-2ebc-448a-93a4-9b0422f6a4e0.png"
     width = "300" height = "300"/>


캡스톤디자인 발표자료 

- 4월 1일 발표 PPT
- 5월 13일 발표 PPT

## 4월 1일 발표 내용

- 주제 설명
- 크롤링이란? (크롤링으로 무엇을 할 것인가)
- 텐서플로우(구글넷) 에 대한 설명
- 이미지 분석 방법(웹캠 카메라 사용)


## 5월 13일 발표 내용


- 추가 수정된 주제 설명
- 팀 내에서 맡은 역할 (모델링)
- 현재 진행 상황 설명
- 향후 계획
 1. 모델링 정확도를 높이기 위해 추가적인 데이터 수집
 2. css작업을 같이 진행하여 웹사이트 완성도 높이기
 3. teachable machine을 먼저 활용 후 모델링 직접 구현


## 모델 소스코드(티처블 머신 활용)
![티처블1](https://user-images.githubusercontent.com/96335258/174133716-e9629ead-58f3-4b1b-a492-76b80e62dbb5.jpg)


<div>Teachable Machine Image Model</div>
<button type="button" onclick="init()">Start</button>
<div id="webcam-container"></div>
<div id="label-container"></div>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@1.3.1/dist/tf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@0.8/dist/teachablemachine-image.min.js"></script>
<script type="text/javascript">
    // More API functions here:
    // https://github.com/googlecreativelab/teachablemachine-community/tree/master/libraries/image

    // the link to your model provided by Teachable Machine export panel
    const URL = "./my_model/";

    let model, webcam, labelContainer, maxPredictions;

    // Load the image model and setup the webcam
    async function init() {
        const modelURL = URL + "model.json";
        const metadataURL = URL + "metadata.json";

        // load the model and metadata
        // Refer to tmImage.loadFromFiles() in the API to support files from a file picker
        // or files from your local hard drive
        // Note: the pose library adds "tmImage" object to your window (window.tmImage)
        model = await tmImage.load(modelURL, metadataURL);
        maxPredictions = model.getTotalClasses();

        // Convenience function to setup a webcam
        const flip = true; // whether to flip the webcam
        webcam = new tmImage.Webcam(200, 200, flip); // width, height, flip
        await webcam.setup(); // request access to the webcam
        await webcam.play();
        window.requestAnimationFrame(loop);

        // append elements to the DOM
        document.getElementById("webcam-container").appendChild(webcam.canvas);
        labelContainer = document.getElementById("label-container");
        for (let i = 0; i < maxPredictions; i++) { // and class labels
            labelContainer.appendChild(document.createElement("div"));
        }
    }

    async function loop() {
        webcam.update(); // update the webcam frame
        await predict();
        window.requestAnimationFrame(loop);
    }

    // run the webcam image through the image model
    async function predict() {
        // predict can take in an image, video or canvas html element
        const prediction = await model.predict(webcam.canvas);
        for (let i = 0; i < maxPredictions; i++) {
            const classPrediction =
                prediction[i].className + ": " + prediction[i].probability.toFixed(2);
            labelContainer.childNodes[i].innerHTML = classPrediction;
        }
    }
</script>

## 링크
티처블 머신 사용해보고 싶은 분들은 아래 링크를 통해 경험해 보세요!

<https://teachablemachine.withgoogle.com/>









