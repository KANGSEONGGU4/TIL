## type 코드
```
type Store = {
  currentPage: number;
  feeds : NewsFeed[];
}
type News = {
  id: number;
  time_ago: string;
  title: string;
  url: string;
  user: string;
  content: string;
}
type NewsFeed = News & {
  comments_count : number;
  points: number;
  read?: boolean;
}

type NewsDetail = News & {
  comments: NewsComment[];
}

type NewsComment = News & {
  comments: NewsComment[];
  level: number;
}
```
## interface 코드
```
interface Store {
  currentPage: number;
  feeds : NewsFeed[];
}
interface News {
  id: number;
  time_ago: string;
  title: string;
  url: string;
  user: string;
  content: string;
}
interface NewsFeed extends News {
  comments_count : number;
  points: number;
  read?: boolean;
}

interface NewsDetail extends News {
  comments: NewsComment[];
}

interface NewsComment extends News {
  comments: NewsComment[];
  level: number;
}
```

#### type vs inferface 차이

- inferface는 "=" 를 쓰지 않는다
- type에서 쓰던 "&" 대신 extends를 사용한다

- type을 쓸지 interface를 쓸지 통일되게 사용해야한다.