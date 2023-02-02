---
id: add-create-page
title: 4. Adding Create Page
tutorial:
    order: 0
    prev: tutorial/adding-crud-pages/{preferredUI}/add-show-page
    next: tutorial/adding-crud-pages/{preferredUI}/add-delete-feature
---

Create page is the page where you can create the record. In this tutorial, we will create the create page for the `products` resource.

## Creating Create Page

First, let's create our file under the `src/pages/products` folder. We will name it `create.tsx`. Then, we will copy the create page code generated by Inferencer and paste it into the file.

To copy the code and paste it into the file, follow the steps below:

1. Navigate to the <a href="http://localhost:3000/products" rel="noopener noreferrer nofollow">localhost:3000/products</a> in your browser.

2. To open the create page, click the "Create" button in the top right corner of the table.

3. On the create page, click on the "Show Code" button in the bottom right corner of the page.

4. You can see the create page code generated by Inferencer. Click on the "Copy" button to copy the code.

5. Paste the code into the you created, `create.tsx` file.

You can see the create page code generated by Inferencer below:

```tsx live previewOnly previewHeight=600px url=http://localhost:3000/products/create
setInitialRoutes(["/products/create"]);

import { Refine } from "@pankod/refine-core";
import {
    Layout,
    ReadyPage,
    notificationProvider,
    ErrorComponent,
} from "@pankod/refine-antd";
import routerProvider from "@pankod/refine-react-router-v6";
import dataProvider from "@pankod/refine-simple-rest";
import { AntdInferencer } from "@pankod/refine-inferencer/antd";

import "@pankod/refine-antd/dist/reset.css";

const App: React.FC = () => {
    return (
        <Refine
            routerProvider={routerProvider}
            dataProvider={dataProvider("https://api.fake-rest.refine.dev")}
            Layout={Layout}
            ReadyPage={ReadyPage}
            notificationProvider={notificationProvider}
            catchAll={<ErrorComponent />}
            resources={[
                {
                    name: "products",
                    list: AntdInferencer,
                    show: AntdInferencer,
                    create: AntdInferencer,
                    edit: AntdInferencer,
                },
            ]}
        />
    );
};

render(<App />);
```

Instead of coding the create page component from scratch, Inferencer've created the required code base on API response, so that we can customize.

## Understanding the Create Component

We will go through the create page components and hooks one by one.

-   `<Create/>` is a **refine** component that is used to presentation purposes like showing the title of the page, save button etc.

    [Refer to the `<Create/>` documentation for more information &#8594](/docs/api-reference/antd/components/basic-views/create)

-   `<Form/>` and `<Form.Item/>` are **Ant Design** components that are used to build the form.

    [Refer to the **Ant Design** `<Form/>` documentation for more information &#8594](https://ant.design/components/form/)

-   `useForm` is a **refine** hook that provides the necessary props for the form. It also provides the `saveButtonProps` prop that we can pass to the submit button of the form.

    When you use `useForm` in the create page, it sends the form data to `dataProvider`'s `create` method when the form is submitted.

    [Refer to the `useForm` documentation for more information &#8594](/docs/api-reference/antd/hooks/form/useForm/)

### Handling Relationships

In the create page, we may need to select a record from another resource. For example, we may need to select a category from the `categories` resource to assign the product to the category. In this case, we can use the `useSelect` hook provided by **refine**. This hook fetches the data by passing the resource name to the `dataProvider`'s `getList` method. Then, it returns the necessary props for the `<Select/>` component.

[Refer to the `useSelect` documentation for more information &#8594](/docs/api-reference/antd/hooks/field/useSelect/)

[Refer to the **Ant Design** `<Select/>` documentation for more information &#8594](https://ant.design/components/select)

In the auto-generated create page code, Inferencer used the `useSelect` hook to select a category from the `categories` resource like below:

```tsx
const { selectProps: categorySelectProps } = useSelect({
    resource: "categories",
});
```

## Adding the Create Page to the App

Now that we have created the create page, we need to add it to the `App.tsx` file.

1. Open `src/App.tsx` file on your editor.

2. Import the created `ProductCreate` component.

3. Replace the `AntdInferencer` component with the `ProductCreate` component.

```tsx title="src/App.tsx"
import { Refine } from "@pankod/refine-core";
import {
    Layout,
    ReadyPage,
    notificationProvider,
    ErrorComponent,
} from "@pankod/refine-antd";
import routerProvider from "@pankod/refine-react-router-v6";
import dataProvider from "@pankod/refine-simple-rest";

import { ProductList } from "pages/products/list";
import { ProductEdit } from "pages/products/edit";
import { productshow } from "pages/products/show";
//highlight-next-line
import { ProductCreate } from "pages/products/create";

import "@pankod/refine-antd/dist/reset.css";

const App: React.FC = () => {
    return (
        <Refine
            routerProvider={routerProvider}
            dataProvider={dataProvider("https://api.fake-rest.refine.dev")}
            Layout={Layout}
            ReadyPage={ReadyPage}
            notificationProvider={notificationProvider}
            catchAll={<ErrorComponent />}
            resources={[
                {
                    name: "products",
                    list: ProductList,
                    edit: ProductEdit,
                    show: ProductShow,
                    //highlight-next-line
                    create: ProductCreate,
                },
            ]}
        />
    );
};
export default App;
```

Now, we can see the create page in the browser at <a href="http://localhost:3000/products/create" rel="noopener noreferrer nofollow">localhost:3000/products/create</a>

<br/>
<br/>

<Checklist>

<ChecklistItem id="add-create-page-antd">
I added the create page to the app.
</ChecklistItem>
<ChecklistItem id="add-create-page-antd-2">
I understood the create page components and hooks.
</ChecklistItem>
<ChecklistItem id="add-create-page-antd-3">
I understood the relationship handling.
</ChecklistItem>

</Checklist>