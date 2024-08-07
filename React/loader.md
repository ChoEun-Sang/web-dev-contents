## loader를 알아보자

서버에 리소스를 요청할 때 항상 반복해야 하는 일종의 보일러 플레이트 코드가 있습니다. 커스텀 훅을 생성해서 반복되는 로직을 줄일 수 있지만, 그럼에도 다양한 HTTP 요청 상태를 처리하고 그 데이터를 가져오기 위해서 반드시 작성해야 하는 코드이 있습니다.

**loader를 사용하면, 컴포넌트를 렌더링하기 전에 데이터를 요청해서 응답받는 데이터를 가지고 컴포넌트를 렌더링하게 됩니다.** 리액트 라우터 버전 6 이상을 사용하고 있다면 데이터를 가져오고 그 다양한 상태들을 처리하는 모든 코드를 작성할 필요가 없습니다.

```js
createBrowserRouter([
  {
    element: <Teams />,
    path: "teams",
    children: [
      {
        element: <Team />,
        path: ":teamId",
        loader: async ({ params }) => {
          return fetch(`/api/teams/${params.teamId}.json`);
        },
      },
    ],
  },
]);
```

## loader()가 리턴한 데이터에 어떻게 액세스할 수 있을까요?

데이터를 사용하려는 컴포넌트에서 loader 함수가 리턴한 데이터에 사용하기 위해 **react-router-dom에서 useLoaderData를 import**할 수 있습니다. useLoaderData는 가장 가까운 loader 데이터에 액세스하기 위해 실행할 수 있는 훅 입니다. **loader() 함수는 Promise를 리턴합니다.**

```js
import { useLoaderData } from "react-router-dom";

export function Team() {
  const TeamData = useLoaderData();
  // ...
}
```

단, **loader 사용한 라우트의 더 높은 수준의 라우트에서는 데이터를 액세스할 수 없습니다.** 만약 상위 수준의 라우트에서 데이터를 엑세스하면 undefined를 반환합니다.

```js
import { useLoaderData } from "react-router-dom";

export function Teams() {
  const TeamData = useLoaderData(); // undefined
  // ...
}
```

## loader() 코드를 어디에 위치시켜야 할까요?

권장사항은 실제로 그 loader 코드를 사용하는 컴포넌트 파일에 넣는 것입니다. 예를 들어, Example 컴포넌트 파일에 loader 함수를 함께 넣습니다.

```jsx
import { useLoaderData } form "react-router-dom";

export default function Example () {
	const loaderData = useLoaderData();

	return <subExample data={loaderData}>
};

export async function loader () {
	const response = await fetch("API URL");

	if (!response.ok) {
		// error handling
	} else {
		const result = await response.json();
		return result
	}
};
```

```jsx
import { RouterProvider, createBrowserRouter } from "react-router-dom";

import Homepage from "./page/Homepage";
// as 키워드를 사용해서 loader 별칭을 사용
import Example, { loader as exampleLoader } from "./page/Example";

const router = createBroswerRouter([
  {
    path: "/",
    element: <RootLayout />,
    children: [
      { index: true, element: <Homepage /> },
      {
        path: "example",
        element: <Example />,
        loader: exampleLoader,
      },
    ],
  },
]);
```

## Loader는 언제 실행되는건가요?

loader는 우리가 페이지로 이동하기 시작할 때 호출됩니다. **React Router는 데이터를 가져올 때까지, 즉 loader가 작업을 완료할 때까지 대기하고, 가져온 데이터로 페이지를 렌더링합니다.**

만약 데이터 응답이 지연된다면, 이벤트가 발생했는데도 아무런 일이 일어나지 않는 것처럼 보일 수 있습니다. 이러한 점을 개선하기 위해 `useNavigation`을 사용할 수 있습니다.

## 응답 지연으로 인한 사용자 경험 개선하기

이벤트가 발생한 후 리액트 `useNavigation` Hook을 사용해서 현재의 라우트 전환 상태를 확인할 수 있습니다. 즉, 전환이 개시되었는지, 우리가 여전히 데이터가 도착하길 기다리고 있는지 이미 다 왔는지 확인할 수 있죠.

useNavigation에서 navigation 객체의 속성을 사용해서 상태를 알아낼 수 있습니다.

```jsx
navigation.state = "idle" | "loading" | "submitting";

// loading 상태일 때 Loading UI를 표시할 수 있다.
```

## loader에서 사용할 수 있는 코드의 종류

loader에서 Web API를 사용할 수 있습니다. 쿠키나 로컬 스토리지에 접근하거나, JS 코드를 사용할 수 있습니다. 단, React 훅은 사용할 수 없습니다.

## errorElement를 이용한 오류 처리

errorElement를 루트 라우트에 추가해서 404 폴백 페이지를 만들거나, 에러 발생시 화면 표시합니다.

children 라우트에도 errorElement를 추가할 수 있습니다. 그럼 해당 라우트에서 에러가 발생할 때만 해당 errorElement를 표시할 수 있습니다.

```jsx
import { RouterProvider, createBrowserRouter } from "react-router-dom";

import Homepage from "./page/Homepage";
// as 키워드를 사용해서 loader 별칭을 사용
import Example, { loader as exampleLoader } from "./page/Example";
import ErrorPage from "./page/Error';

const router = createBroswerRouter([
{
	path: "/",
	element: <RootLayout />,
	errorElement: <ErrorPage />
	children: [
		{ index: true, element: <Homepage />},
		{
			path: "example",
			element: <Example />,
			loader: exampleLoader
		}
	]
}
])
```

## useRouteError 훅 사용해서 thorw new Response(에러객체) 처리하기

```jsx
// Route에서 발생한 에러를 훅을 통해 겍체로 받을 수 있다.
import { useRouteError } from "reat-route-dom";

const Error = () => {
  const error = useRouteError();

  let title = "An error occurred!";
  let message = "Something went wrong!";

  // loader에서 throw new Response 한 JSON 객체 처리하기
  if (error.status === 500) {
    message = JSON.parse(error.data).message;
  }

  // 경로 못 찾는 경우, 기본적으로 404 에러 발생
  if (error.status == 404) {
    title = "Not Found";
    message = "Could not find resource or page";
  }

  return (
    <>
      // 페이지 네비게이션을 추가하면 // 에러 페이지에서 다른 페이지로 이동할 수
      있어서 사용자 경험 향상
      <Navigation />
      <PageContent title={title}>
        <p>{message}</p>
      </PageContent>
    </>
  );
};

export default Error;
```

```jsx
import { useLoaderData } form "react-router-dom";

export default function Example () {
	const loaderData = useLoaderData();

	if (loaderData.isError) {
		console.log(loaderData.message);  // Could not fetch data
	}

	return <subExample data={loaderData}>
};

export async function loader () {
	const response = await fetch("API URL");

	if (!response.ok) {
		throw new Response(JSON.stringify({message:  "Could not fetch data"}),
		{status: 500}
		)
	} else {
		const result = await response.json();
		return result
	}
};
```

### Json() 유틸리티 함수

new Response를 사용하는 대신 json 유틸리티 함수를 사용하면 코드도 줄어들고 가독성이 좋아집니다.

```jsx
import { useLoaderData, json } form "react-router-dom";

export default function Example () {
	const loaderData = useLoaderData();

	if (loaderData.isError) {
		console.log(loaderData.message);  // Could not fetch data
	}

	return <subExample data={loaderData}>
};

export async function loader () {
	const response = await fetch("API URL");

	if (!response.ok) {
		return json({message: "데이터 통신 오류"},{status: 500})
	} else {
		const result = await response.json();
		return result
	}
};
```

```jsx
const error = useRouteError();
//  json 객체 처리하기
if (error.status === 500) {
  const message = error.data.message;
}
```

## 동적 라우트와 loader()

loader는 파라미터로 객체를 전달하는데, 객체에서 request와 params에 접근할 수 있습니다. request 값을 통해 url 등의 값에 접근할 수 있고, params로 동적 라우트 파라미터에 접근할 수 있습니다.

```jsx
function loader({ request, params }) {
  const id = params.eventId;

  const res = fetch("BASE URL" + id);

  if (!res.ok) {
    return json({ message: "NO DATA" }, { status: 500 });
  } else {
    return res;
  }
}
```

> _가장 일반적인 사용 사례는 [URL을](https://developer.mozilla.org/en-US/docs/Web/API/URL) 생성하고 여기에서 [URLSearchParams를](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 읽는 것입니다 ._
>
> ```jsx
> function loader({ request }) {
>   const url = new URL(request.url);
>   const searchTerm = url.searchParams.get("q");
>   return searchProducts(searchTerm);
> }
> ```
>
> _여기의 API는 React Router에 특화된 것이 아니라 표준 웹 객체( [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) , [URL](https://developer.mozilla.org/en-US/docs/Web/API/URL) , [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) )입니다 ._

## useRouteLoaderData

> _이 후크는 **현재 렌더링된 경로의 데이터를 트리의 어디에서나 사용**할 수 있게 합니다. 이는 트리의 깊은 곳에서 훨씬 더 위쪽 경로의 데이터가 필요한 구성 요소와 트리의 더 깊은 곳에 있는 자식 경로의 데이터가 필요한 부모 경로에 유용합니다._

useLoaderData는 해당 컴포넌트가 특정 라우트에 매핑될 때, 이 라우트에 정의된 loader 함수가 데이터를 반환하고, useLoaderData를 사용하여 이 데이터를 접근할 수 있습니다.

하지만, 현재 라우트가 아닌 다른 라우트의 loader 데이터도 접근하기 위해서는 useRouteLoaderData 사용해야 합니다.

이 부모 라우트의 데이터를 사용하려면 부모 라우트에 id 프로퍼티를 추가해야 합니다. 이 훅은 useLoaderData와 거의 비슷하게 작동하지만, routeId를 인자로 받습니다.

```jsx
createBrowserRouter([
  {
    path: "/",
    loader: () => fetchUser(),
    element: <Root />,
    id: "root",
    children: [
      {
        path: "jobs/:jobId",
        loader: loadJob,
        element: <JobListing />,
      },
    ],
  },
]);
```

```jsx
const user = useRouteLoaderData("root");
```

> _사용 가능한 유일한 데이터는 현재 렌더링된 경로입니다. 현재 렌더링되지 않은 경로에서 데이터를 요청하면 후크가 `undefined`을 반환합니다_

## 참고

[[react-router-dom 공식문서]](https://reactrouter.com/en/main/route/loader)
