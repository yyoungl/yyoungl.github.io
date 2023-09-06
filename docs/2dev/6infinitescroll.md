---
layout: default
title: Cursor based Pagination - Infinite Scroll 구현 (React, Scroll Event)
nav_order: 6
parent: Project
---

# **Cursor based Pagination - Infinite Scroll 구현 (React, Scroll Event)**

커서 기반 페이지네이션 구현 과정 - 스크롤 탐지 이벤트로 무한 스크롤 페이지 만들기

![엘리스 AI트랙 7기 2차 프로젝트: 채식 장려 커뮤니티 <오채완> (1)](https://letusgrow.tistory.com/25)

엘리스 AI 7기 2차 프로젝트를 진행하면서 인피니트 스크롤을 구현했다. 시간이 꽤 지났지만 도전했던 부분들에 대해 하나씩 써보려 한다. 첫 번째로 가장 기억에 남는 무한 스크롤이다.

### **프로젝트 내 적용된 파일들**

[전체 게시물 페이지](https://github.com/yyoungl/VegCom-elice-2nd-project-front/blob/master/src/pages/story/story.jsx)

[게시물 검색 페이지](https://github.com/yyoungl/VegCom-elice-2nd-project-front/blob/master/src/pages/story/searchpost.jsx)

[게시물 상세 - 댓글 무한 스크롤](https://github.com/yyoungl/VegCom-elice-2nd-project-front/blob/master/src/components/post/postdetail.jsx)

![결과물 - 용량 이슈로 스크롤까지는 안 보이지만 푸터가 등장하자마자 새로운 글이 뜬다!!](https://blog.kakaocdn.net/dn/bmxgP1/btstgjjODuR/igOrWuVDxFK6eHWKdisss0/img.gif)

결과물 - 용량 이슈로 스크롤까지는 안 보이지만 푸터가 등장하자마자 새로운 글이 뜬다!!

## **Contents**

1. 구현 배경
2. 논리 구조
3. offset 방식 vs cursor 방식
4. Scroll Event
5. Cursor Based Pagination
6. 마무리 & Full Solution

# **1) 구현 배경**

2차 프로젝트를 하던 중 사용자들이 포스트를 올리는 피드 페이지 `story.jsx` 를 생성했다. 사진이 꼭 들어있어야 글을 올릴 수 있었기 때문에 포스트가 점점 늘면 페이지 로드 후 한꺼번에 불러오기에는 무리가 있었다.

게시물을 보여주는 페이지를 나눠서 사용자가 직접 페이지를 넘길 수도 있었지만, 우리는 페이스북이나 인스타그램 피드 같은 화면을 원했기 때문에 인피니트 스크롤을 구현하기로 했다.

인터넷에 검색해 보면 구현할 수 있는 라이브러리 같은 게 많다고 들었지만 직접 생각하고 만들어 보려고 하루를 꼬박 썼다.

# **2) 논리 구조**

논리 구조는 생각해 보면 간단하다.

1. 페이지가 로드될 때 우리가 정해 둔 개수만큼 글을 보여준다.
2. Scroll Event를 이용해서 화면의 마지막에 도달한다면 GET 요청을 보낸다.
3. 이전에 있었던 게시물 목록 + 새로 받아온 게시물 목록
4. server에서 더이상 게시물이 없다는 신호를 보내면 보여줄 글이 더 없다는 뜻이므로 요청을 멈춘다.

# **3) offset 방식 vs cursor 방식**

매일 피드백을 주시던 코치님께서 인피니트 스크롤을 구현할 때, 데이터를 처리하는 과정에서 오프셋을 주고받으며 구현하면 된다고 하셨다. 하지만 우리의 DB 구조상 오프셋을 가지고 구현하기에는 문제가 있었다.

우리는 게시물이 새로 생성될 때 increment 방식으로 아이디를 부여했다. 글이 써진 순서대로 1부터 하나씩 커지는 숫자를 부여받는 것이다. 결론적으로 우리는 이를 기반으로 cursor 방식을 선택했다.

초반에 백엔드 팀원들과 함께 이야기하면서 서로 offset과 cursor 방식으로 할 거라고 다르게 생각하고 있어서 그것부터 확실하게 정해야 했다. ㅋㅋㅋㅋ

### **offset 방식**

offset 방식의 경우 클라이언트에서 가져오고 싶은 데이터의 시작 위치를 나타내는 `offset`과 전달받길 원하는 데이터의 개수 `limit`을 전달하여 `limit` 크기를 가지는 배열을 전달받는 방식이다.

offset 방식을 사용할 때 발생할 수 있는 문제점으로, offset은 전체 게시물 목록 중 해당 게시물의 상대적인 위치를 나타내기 때문에 현 프로젝트처럼 실시간으로 글 목록에 새로운 게시물이 추가되고 삭제될 경우 글을 제대로 볼 수 없다는 것이다.

처음 페이지가 로드될 시점에 전체 글이 12개 있다고 생각해 보자. (limit은 5라고 가정)

처음에는 가장 최근에 등록된 8번째~12번째의 글이 조회된다. 하지만 사용자가 차근차근 하나씩 보고 있던 도중, 13번째 글이 올라왔다면? 스크롤이 가장 밑에 도달했을 때 API 요청을 시간순으로 6번째 게시물~10번째 게시물을 요청한다. 그래서 화면에는 8번째 글이 2개 보이게 된다.

따라서 현재 새로운 게시물이 올라왔는지, 안 올라왔는지 확인하고 가지고 있지 않으려면,

**게시물 전체 목록의 길이가 변해도 달라지지 않는 값이 필요하다.**

### **cursor 방식**

cursor 방식은 **마지막으로 받은 게시물의 id**만을 가지고 있다가, 이를 바탕으로 다음 게시물을 요청하는 것이다. 우리는 게시물의 id 작성 시간순으로 부여했기 때문에 서버에서는 마지막 게시물의 id보다 큰 id (마지막 커서의 게시물보다 늦게 작성된 게시물) 를 갖는 게시물들을 순차적으로 보내 주면 된다.

이를 통해 데이터가 더 있는지, 없는지도 판단할 수 있다. 만약 더 받을 데이터가 없을 경우 response에 -1 (게시물의 인덱스로 가질 수 없는 값) 을 보냄으로써 GET 요청을 멈추는 방식으로 구현했다.

# **4) Scroll Event**

페이지의 마지막을 감지하고, 마지막을 감지했을 때, 그리고 페이지가 처음 로드되었을 때 GET 요청을 보내는 Hook, 이때 `nextCursor`의 초기값을 0으로 설정해 두고 요청을 보냈다.

`isReached`를 `fetchPost` 훅의 의존성으로 설정해 상태가 변경될 때마다 다시 요청을 보내는 방식이다. (true든 false든 상태가 바뀌기만 하면 요청을 보낼 줄 알았는데 이것은 큰 오산이었다….)

```jsx
const handleScroll = useCallback(() => {
  const scrollHeight = document.documentElement.scrollHeight;
  const scrollTop = document.documentElement.scrollTop;
  const clientHeight = document.documentElement.clientHeight;

  if (scrollTop + clientHeight >= scrollHeight) {
    setIsReached(true);
  }
}, []);

useEffect(() => {
  // 페이지 초기 렌더링 시에 postList를 불러오기 위해 fetchPost 호출
  fetchPost(nextCursor);
  // 스크롤 이벤트 핸들러 등록 및 해제
  window.addEventListener("scroll", handleScroll);
  return () => {
    window.removeEventListener("scroll", handleScroll);
  };
}, [fetchPost]);
```

# **5) Cursor Based Pagination**

`fetchPost` Hook의 로직은 크게 이렇게 이루어져 있다. 우리는 게시물을 5개씩 받아와서 보냈고, 댓글의 경우 10개씩 받아와서 보냈다.

1. 페이지 마지막에 도달했다는 것을 탐지 → Hook 재정의
2. 이전에 갱신된 cursor의 값이 -1 인지 확인 (더 이상 볼 글이 없다는 뜻)

   -1이라면 더 이상 요청을 보내지 않고 return

   ```jsx
   if (cursor === -1) {
     setIsLoading(false);
     return;
   }
   ```

3. cursor 값을 Api 요청 url에 넣어 요청을 보낸다.
4. 결과값을 바탕으로 nextCursor를 갱신한다.

   받은 게시물의 개수가 5개 미만이라면 마지막 부분이라는 뜻이므로 더 이상 요청을 보내지 않기 위해 cursor를 -1로 설정한다.

   5개 이상인 경우, 새로 받아 온 데이터 리스트의 마지막 원소의 아이디를 nextCursor로 설정한다.

   ```jsx
   const res = await getApi(`post/list/${cursor}`);

   const postData = res.data;

   if (postData.postList?.length < 5) {
     setNextCursor(-1);
   } else {
     setNextCursor(postData.postList[postData.postList.length - 1].postId);
   }
   ```

5. 게시물 목록인 postList도 갱신 - cursor와 게시물 리스트의 길이를 기반으로 다르게 판단

   현재 cursor가 0인 경우 페이지가 처음 로드되었거나 새로고침되었을 때를 의미하기 때문에 새로운 리스트를 만들어 줘야 한다.

   cursor가 0보다 크고, 새로 받아온 리스트의 길이가 0보다 클 경우에는

   `이전 리스트 + 새로 받아온 리스트`를 합쳐야 하기 때문에 이 방식으로 갱신해 준다.

   만약, 전체 게시물의 개수가 5의 배수만큼 있어서 새로 받아온 게시물 리스트의 길이가 0일 경우에는, 원래 있는 리스트를 그대로 보여 준다.

   ```jsx
   let newPostList;

   if (cursor === 0) {
     newPostList = postData.postList;
   } else if (cursor > 0 && postData.postList.length > 0) {
     newPostList = [...postList, ...postData.postList];
   } else if (postData.postList.length === 0) {
     newPostList = [...postList];
   }

   setPostList(newPostList);
   ```

더 이상 보여줄 글이 없음에도 요청이 계속 들어가서 아무것도 없는 리스트로 갱신되어 화면에 아무것도 안 나오기도 하고, 페이지 로드 후 GET 요청을 2번 보내서 혼자 10개의 글이 나오기도 했다…. 커서와 의존성 이슈였던 걸로 기억한다.

# **6) 마무리 & Full Solution**

코치님께서 이 코드 자체가 이상적인 코드는 아니라고 하셨지만, ‘주문하면 나오는 팀’ 이라는 피드백을 듣기도 했다. ㅎㅎ 만들고자 하는 것에 대해 어떻게 하면 구현할 수 있을지, 그리고 만드는 로직을 생각해 보고 직접 만들어 보며 마음처럼 되지 않는 과정도 겪어 보았다. 1차 프로젝트에서도 느꼈지만, 시행착오를 겪는 시간이 있기 때문에 이후에 같은 기능을 구현할 때 더 효율적으로 할 수 있게 성장하는 것 같다.

```jsx
function Story() {
  const navigate = useNavigate();
  const [postList, setPostList] = useState([]);
  const [nextCursor, setNextCursor] = useState(0);
  const [isLoading, setIsLoading] = useState(false);
  const [isReached, setIsReached] = useState(false);

  const fetchPost = useCallback(
    async (cursor) => {
      try {
        if (cursor === -1) {
          setIsLoading(false);
          return;
        }
        setIsLoading(true);

        const res = await getApi(`post/list/${cursor}`);

        const postData = res.data;

        if (postData.postList?.length < 5) {
          setNextCursor(-1);
        } else {
          setNextCursor(postData.postList[postData.postList.length - 1].postId);
        }

        let newPostList;

        if (cursor === 0) {
          newPostList = postData.postList;
        } else if (cursor > 0 && postData.postList.length > 0) {
          newPostList = [...postList, ...postData.postList];
        } else if (postData.postList.length === 0) {
          newPostList = [...postList];
        }

        setPostList(newPostList);

        setIsReached(false);
      } catch (err) {
        if (err.response.data.message) {
          alert(err.response.data.message);
        } else {
          alert("라우팅 경로가 잘못되었습니다.");
        }
      } finally {
        setIsLoading(false);
      }
    },
    [isReached]
  );

  const handleScroll = useCallback(() => {
    const scrollHeight = document.documentElement.scrollHeight;
    const scrollTop = document.documentElement.scrollTop;
    const clientHeight = document.documentElement.clientHeight;

    if (scrollTop + clientHeight >= scrollHeight) {
      setIsReached(true);
    }
  }, []);

  useEffect(() => {
    // 페이지 초기 렌더링 시에 postList를 불러오기 위해 fetchPost 호출
    fetchPost(nextCursor);
    // 스크롤 이벤트 핸들러 등록 및 해제
    window.addEventListener("scroll", handleScroll);
    return () => {
      window.removeEventListener("scroll", handleScroll);
    };
  }, [fetchPost]);

  return (
    <div className="flex justify-center" style={{ width: "900px" }}>
      <div>
        <div className="justify-center flex items-center mx-auto max-w-2xl lg:mx-0">
          <h2 className="text-3xl w-full font-bold tracking-tight text-gray-900 sm:text-4xl mb-10">
            함께 실천하는 사람들을 만나 보세요.
          </h2>
        </div>
        <div className="flex mb-10" style={{ justifyContent: "center" }}>
          <div
            className="searchButton w-auto mr-5"
            onClick={() => navigate("/searchPost")}
          >
            검색하기
          </div>
          <div
            className="addPostButton btn-2 w-auto "
            onClick={() => navigate("/addpost")}
          >
            식단 기록하기
          </div>
        </div>
        {postList.map((post) => (
          <div key={post.postId}>
            <PostCard post={post} />
          </div>
        ))}
        {isLoading && <p>Loading...</p>}
      </div>
    </div>
  );
}
```
