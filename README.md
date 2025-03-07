## 안전하지 않은 캡챠
이 도구를 이용하여 허용받지 않은 서비스 대상으로 해킹을 시도하는 행위는 범죄 행위 입니다. 해킹을 시도할 때에 발생하는 법적인 책임은 그것을 행한 사용자에게 있다는 것을 명심하시기 바랍니다.      
Insecure CAPTCHA 캡차는 컴퓨터가 알 수 없는 흘려 쓴 글씨나, 그림등의 클릭 키를 입력받아서 사람인지 확인하는 것입니다.     
쉽게 말해 사이트에서 사람이 접근하려고 하는 것인지 봇이 접근하는 것인지 판단하기 위하여 많이 사용되고 있습니다.      

Insecure CAPTCHA 문제의 화면입니다. 해당 취약점 진단을 하기위해서는 캡차 설정을 해야 합니다.        
먼저 메모장으로 config.inc.php 파일을 열어주신후 밑에 보이시는 링크를 눌러 해상 사이트에 접속을 해줍니다.         

사이트를 접속하시면 다음과 같은 화면이 보이실 겁니다. 해당 칸에 맞춰 작성을 하신후 [Register] 버튼을 눌러 줍니다.     

해당 버튼을 눌러 주시면  Site Key, Secret Key 가 각각 발급이 되고, 이제 해당 키값을 아까 메모장으로 열어 놓았던 config.inc.php 파일안에 넣어 줘야 합니다.    

recaptcha_public_key = Site Key, recaptcha_private_key = Secret Key 넣어 주신후 저장하고 웹페이지를 새로고침 해줍니다.   

다음과 같은 화면이 뜨셨다면 캡차 등록이 정상적으로 되신겁니다.    

#### Low레벨
Low레벨의 소스코드를 보면 step ==1 값과 step==2 값이 있는데 실제 패스워드 변경후 성공되었을경우 step==2의 값으로 보내는것을 확인할수 있습니다. 그럼 여기서 버프스위트를 통해 캡차 우회를 해보도록 하겠습니다.    

간단하게 패스워드만 입력후 버프스위트에서 패킷을 잡은 모습입니다. 여기서 step 값을 2로 변경해주신후 [Forward] 버튼으로 프록시를 넘겨주면 캡차인증없이 간단히 패스워드가 변경되는 모습을 볼수 있습니다.    

#### Medium레벨
Medium레벨의 소스코드에서는 passed_captcha 가 추가된 것을 볼 수 있습니다. 여기서도 마찬가지로 버프스위트를 이용하여 우회가 가능합니다.     
step=2&password_new=password&password_conf=password&passed_captcha=true&Change=Change 이렇게 추가해 주신후 패킷을 넘겨주면 정상적으로 변경된 모습을 보실수 있습니다. 이 부분은 직접 해보시기 바랍니다.     

#### High레벨
High레벨의 소스코드를 보시면 if 문을 통해 캡차 값과 User Agent 조건을 검사를 하고 있습니다.     
여기서도 버프스위트를 통해 우회가 가능합니다. 일단 User Agent 값과 g-recaptcha-response 값을 변경후 패킷을 넘겨주면 패스워드를 바꾸실 수 있습니다.     

## More Information
https://en.wikipedia.org/wiki/CAPTCHA
https://www.google.com/recaptcha/
https://www.owasp.org/index.php/Testing_for_Captcha_(OWASP-AT-012)
