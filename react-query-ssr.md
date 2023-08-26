# React-Query SSR (prefetchQuery vs fetchQuery)

- Next js의 SSR (getServerSideProps) 에서 React-Query 사용하고 싶다면 _app.tsx 파일의 클라이언트 측에서 아래와 같이 Hydrate 으로 묶으면 되고,

```
export default function MyApp({ Component, pageProps }) {
  const [queryClient] = React.useState(() => new QueryClient());

  return (
    <QueryClientProvider client={queryClient}>
      <Hydrate state={pageProps.dehydratedState}>
        <Component {...pageProps} />
      </Hydrate>
    </QueryClientProvider>
  );
}
```

<br />

- API를 호출하고자 하는 페이지의 getServerSideProps에서 api를 호출한 후 dehydrate로 묶은 후 props로 전달하면 됩니다. 여기까지는 간단한 거죠.

```
export async function getStaticProps() {
  const queryClient = new QueryClient()

  await queryClient.prefetchQuery(['posts'], getPosts)

  return {
    props: {
      dehydratedState: dehydrate(queryClient),
    },
  }
}
```

<br />

- 여기서 getServerSideProps 부분에서 prefetchQuery 를 사용할 수도 있고, fetchQuery 를 사용할 수도 있습니다. 이 둘의 차이는 다음과 같다고 합니다.
  - queryClient.prefetchQuery: prefetchQuery is an asynchronous method that can be used to prefetch a query before it is needed or rendered with useQuery and friends. The method works the same as fetchQuery except that it will not throw or return any data.
  - prefetchQuery 는 query의 값이 화면에 렌더링되기 이전 호출할 때 사용하는 것으로,  fetchQuery 와 같은 방식으로 작동하는데 리턴 값이 없고 에러를 던지지 않는다는 점에서만 차이가 있습니다.
  - queryClient.fetchQuery: fetchQuery is an asynchronous method that can be used to fetch and cache a query. Use the prefetchQuery method if you just want to fetch a query without needing the result.
  - fetchQuery 는 비동기 함수로 fetch하고 cache하는 데에 사용하는 것으로, 쿼리의 결과가 필요하지 않으면 prefetchQuery 를 쓰면 됩니다.

<br />
 
- 쉽게 말해 서버사이드에서 api의 결과를 사용하거나 에러 여부를 확인하고 싶으면 getServerSideProps에서 fetchQuery를 사용하고, 그럴 필요가 없으면 prefetchQuery를 사용하면 됩니다.

<br />

- 출처
  - [SSR | TanStack Query Docs](https://tanstack.com/query/v4/docs/react/guides/ssr#using-hydration)
  - [QueryClient | TanStack Query Docs](https://tanstack.com/query/v4/docs/react/reference/QueryClient#queryclientfetchquery)

