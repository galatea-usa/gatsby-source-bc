## Features

- Support for both `v2` and `v3` BigCommerce API versions

## Installation and Setup

For `npm`:

```console
npm install @edl/gatsby-source-bigcommerce
```

For `yarn`:

```console
yarn add @edl/gatsby-source-bigcommerce
```

Setup this plugin in `gatsby-config.js` as follows:

```javascript
module.exports = {
	plugins: [
		{
			resolve: "@edl/gatsby-source-bigcommerce",
			options: {
				clientId: process.env.BIGCOMMERCE_API_CLIENT_ID,
				secret: process.env.BIGCOMMERCE_API_SECRET,
				accessToken: process.env.BIGCOMMERCE_API_ACCESS_TOKEN,
				storeHash: process.env.BIGCOMMERCE_API_STORE_HASH,
				endpoints: {
					BigCommerceProducts: "/v3/catalog/products?include=images,variants,custom_fields,options,modifiers,videos",
					BigCommerceCategories: "/v3/catalog/categories",
					BigCommerceCategoriesTree: "/v3/catalog/categories/tree",
					BigCommerceBrands: "/v3/catalog/brands"
				}
			}
		}
	]
};
```

## Configuration Options

Add a single or multiple `endpoints`. You can find a list of endpoints [here](https://developer.bigcommerce.com/api-reference/).

```javascript
options: {
	...

	// Required fields
	clientId: process.env.BIGCOMMERCE_API_CLIENT_ID,
	secret: process.env.BIGCOMMERCE_API_SECRET,
	accessToken: process.env.BIGCOMMERCE_API_ACCESS_TOKEN,
	storeHash: process.env.BIGCOMMERCE_API_STORE_HASH,

	// Create a node name and map it to a valid `bigcommerce` endpoint
	endpoints: {
		// Single endpoint
		BigCommerceProducts: "/v3/catalog/products?include=images,variants,custom_fields,options,modifiers,videos",

		// Multiple endpoints
		BigCommerceCategories: "/v3/catalog/categories",
		BigCommerceCategoriesTree: "/v3/catalog/categories/tree",
		BigCommerceBrands: "/v3/catalog/brands"
	}
}
```

## How to Query

Assuming you correctly setup the plugin in `gatsby-config.js` and you have a `BigCommerceProducts` node name and its valid endpoint:

```javascript
endpoints: {
	BigCommerceProducts: "/v3/catalog/products?include=images,variants,custom_fields,options,modifiers,videos";
}
```

you can query the data as follows:

```graphql
{
	allBigCommerceProducts {
		nodes {
			name
			price
			id
			sku
			variants {
				id
				product_id
				price
				cost_price
				image_url
				sku
			}
			reviews_count
			reviews_rating_sum
			page_title
			images {
				id
				description
				product_id
				date_modified
			}
			bigcommerce_id
			brand_id
			custom_url {
				url
			}
			categories
			availability
		}
		totalCount
	}
}
```

## GraphQL

- You can access the GraphQL Playground by visiting `localhost:8000/__graphql`, assuming you already run your `gatsby` site.
