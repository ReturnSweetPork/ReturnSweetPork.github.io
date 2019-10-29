# Django modeling(평판 모델링 생성 및 기능구현)



평판 기능 구현 아이디어



평판 목록 (energetic, humorous, leadership, gentle) 선택시 숫자 1을 부여



기존 유저 모델에 userFame 을 추가함.



```python
class User(models.Model):
    userName = models.CharField(max_length=100)
    userNickName = models.CharField(max_length=100)
    userId = models.CharField(max_length=50)
    userSex = models.CharField(max_length=20)
    userAge = models.CharField(max_length=50)
    userImage = models.ImageField(blank=True)
    userGrade = models.IntegerField(default=1)
    userAddress = models.CharField(max_length=200, blank=True)
    userPoint = models.IntegerField(default=0)
    userLike = ArrayField(
        ArrayField(
            models.CharField(max_length=50, blank=True, default=''),
            size=8,
            blank=True,
            default=list,
            null=True
        ),
        size=2,
        blank=True,
        null=True
    )
    #평판 추가
    userFame = [0,0,0,0]

    def __str__(self):
        return self.userName
```





userFame 을 리스트 형식인 [0,0,0,0] 형식으로 작성하여



평판 선택시 1씩 추가해주는 방식으로 기능구현예정



```python
#views.py 작성

#평판 점수 수정(한명이 한개의 평판을 줄때 그것을을 1로 산정해서 추가해줌, defalt=0)
@api_view(['POST'])
def fame_update(request, post_id):
    #post_id 는 현재 유저가 포함되어있는 모임의 아이디입니다.
    #print(request.data)
    #request.data는 데이터 형식임을 확인합니다.
    
    userList = ParticipantCheck.objects.filter(post_id = post_id).values()
    #유저가 속해있는 모임과 같은 아아디를 가진 오브젝트를 가져옴
    print(userList)
    #dic형식의 userList를 확인하였습니다.
    for i in userList:
        user = User.objects.get(id=i.get('user_id'))
        print(i.get('user_id'))
        #user_id는 숫자형태입니다. id값
        print(user)
        #user는 user_id로 확인한 실제 유저의 이름입니다.
    #만일 POST 방식으로 데이터가 들어왔을 경우 이 값이 "vote" : "어떠한 평판인가" 의 경우에 맞추어서 1씩 값을 추가해줌.
    if request.data.get("vote") == 'energetic':
        user.userFame[0] += 1
    elif request.data.get("vote") == 'humorous':
        user.userFame[1] += 1
    elif request.data.get("vote") == 'leadership':
        user.userFame[2] += 1
    elif request.data.get("vote") == 'gentle':
        user.userFame[3] += 1
        
    #유저값을 저장함
    user.save()
    pass
```



결과적으로 [0,0,0,0] 에서



[0,0,1,0] 등으로 변경되는것을 확인할수 있었다.



하지만 다시한번 함수를 실행하였을때 [0,0,0,0] 으로 초기화되는 오류가 있어 현재는 수정중입니다.





