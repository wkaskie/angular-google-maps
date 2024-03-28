+++
date = "2017-08-31T13:51:15-05:00"
draft = false
title = "Markers cluster with Marker Clusterer – A Google Maps JavaScript API utility library"
+++

Angular Google Maps provides a package that allows you to use [markerclustererplus](https://github.com/googlemaps/v3-utility-library/tree/master/markerclustererplus) together with @wafka/agm-core. 'Marker Clustererc' allows you to create and manage per-zoom-level clusters for large amounts of markers.

## Install the needed packages
First make sure that you install the following NPM packages:

```bash
npm install @wafka/agm-core @wafka/agm-markerclusterer @google/markerclustererplus
```

Remember to add `--save` if you want npm to store the package in your packaje.json

Make sure you have a Google Maps API Key - [you can get one here](https://developers.google.com/maps/documentation/javascript/get-api-key).

## Update angular.json

If you want to use default icons, you must add the following entry to the asset's property array (`projects/<yourproject>/architect/build/options/assets`) in angular.json:

```json
{"input": "./node_modules/@google/markerclustererplus/images", "glob": "*", "output": "/images"}
```

## Loading the modules

Update your root component (e.g. src/app/app.module.ts) and import the following modules:

```typescript
import { AgmCoreModule } from '@wafka/agm-core';
import { AgmMarkerClustererModule } from '@wafka/agm-markerclusterer';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AgmCoreModule.forRoot({
      apiKey: ['YOUR_API_KEY_HERE']
    }),
    AgmMarkerClustererModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## Using the directive

When you import the `AgmMarkerClustererModule`, you can use the `agmMarkerCluster` directive  in your template. 

```html
<agm-map style="height: 300px" [latitude]="51.673858" [longitude]="7.815982">
  <agm-marker-cluster>
    <agm-marker *ngFor="let marker of markers" [latitude]="marker.latitude" [longitude]="marker.longitude"></agm-marker>
  </agm-marker-cluster>
</agm-map>
```

### Specifying a custom calculator

If you want to control how the cluster style is calculated, you can pass in a `CalculateFunction` via `calculator`:

```html
<agm-map [latitude]="0" [longitude]="0">
  <agm-marker-cluster [calculator]="myCalculatorFn">
    <agm-marker *ngFor="let marker of markers" [latitude]="marker.latitude" [longitude]="marker.longitude"></agm-marker>
  </agm-marker-cluster>
</agm-map>
```
