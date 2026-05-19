# Guía Paso a Paso — Examen Parcial: The Wine Square
### Curso: Desarrollo de Aplicaciones Open Source (1ASI0729) | NRC: 20262

---

## PASO 1 — Creación del Proyecto Angular

**Cargar** el Terminal del sistema operativo, ubicarse en la carpeta de preferencia y **ejecutar**:

```bash
ng new ea20262u<TU-CODIGO>
```

> Reemplaza `<TU-CODIGO>` con tu código de estudiante en minúsculas. Ejemplo: `ea20262u202112345`

_? Which stylesheet format would you like to use?_, **Seleccionar**:
```
CSS
```

_? Do you want to enable Server-Side Rendering (SSR) and Static Site Generation (SSG/Prerendering)?_, **digitar**:
```
N
```

_? Do you want to create a 'zoneless' application without zone.js? (y/N)_, **digitar**:
```
Y
```

_? Which AI tools do you want to configure with Angular best practices?_, **Seleccionar ambas con `<space>`**:
```
(*) GitHub Copilot
(*) JetBrains AI Assistant
```

---

## PASO 2 — Instalación de Angular Material

**Ingresar** a la carpeta del proyecto:
```bash
cd ea20262u<TU-CODIGO>
```

**Ejecutar**:
```bash
ng add @angular/material
```

_? Would you like to proceed? (Y/n)_, **digitar**:
```
Y
```

_? Choose a prebuilt theme name, or "custom" for a custom theme:_, **seleccionar**:
```
Deep Purple/Amber
```

---

## PASO 3 — Instalación de dependencias adicionales

### Internationalization (i18n)
```bash
npm install @ngx-translate/core @ngx-translate/http-loader --save
```

### JSON Server
```bash
npm install -g json-server@0.17.4
```

---

## PASO 4 — Creación de los Archivos de idiomas

**Crear** las carpetas `assets` e `i18n` dentro de `public/`:

```markdown
- 📂 public
  - 📁 assets
    - 📁 i18n
```

**Crear** los archivos `en.json` y `es.json` en la carpeta `i18n`:

### `public/assets/i18n/en.json`

```json
{
  "option": {
    "home": "Home",
    "new-preservation-item": "New Preservation Item"
  },
  "toolbar": {
    "title": "The Wine Square Cellar Management Platform"
  },
  "home": {
    "title": "Home",
    "content": "Engineered Products for Wine Cellars.",
    "my-wine-cellars": "My Wine Cellars",
    "empty": "Empty",
    "total-bottles": "Total Bottles",
    "available-capacity": "Available Capacity"
  },
  "preservation": {
    "title": "New Preservation Item",
    "subtitle": "Add Wine Bottles to Your Cellar",
    "wine-type": "Wine Type",
    "wine": "Wine",
    "quantity": "Quantity",
    "create": "Create",
    "cancel": "Cancel",
    "quantity-required": "Quantity is required",
    "quantity-exceeded": "Quantity exceeds available capacity",
    "wine-required": "Wine is required",
    "wine-type-required": "Wine type is required"
  },
  "page-not-found": {
    "title": "Page not found",
    "content": "The path <strong>{{ invalid_path }}</strong> is not valid.",
    "go-home": "Go Home"
  },
  "footer": {
    "rights": "All rights reserved.",
    "powered-by": "Powered by",
    "and": "and"
  }
}
```

### `public/assets/i18n/es.json`

```json
{
  "option": {
    "home": "Inicio",
    "new-preservation-item": "Nuevo Item de Preservación"
  },
  "toolbar": {
    "title": "The Wine Square Plataforma de Gestión de Bodegas"
  },
  "home": {
    "title": "Inicio",
    "content": "Productos Diseñados para Bodegas de Vino.",
    "my-wine-cellars": "Mis Bodegas de Vino",
    "empty": "Vacío",
    "total-bottles": "Total de Botellas",
    "available-capacity": "Capacidad Disponible"
  },
  "preservation": {
    "title": "Nuevo Item de Preservación",
    "subtitle": "Añadir Botellas de Vino a tu Bodega",
    "wine-type": "Tipo de Vino",
    "wine": "Vino",
    "quantity": "Cantidad",
    "create": "Crear",
    "cancel": "Cancelar",
    "quantity-required": "La cantidad es requerida",
    "quantity-exceeded": "La cantidad supera la capacidad disponible",
    "wine-required": "El vino es requerido",
    "wine-type-required": "El tipo de vino es requerido"
  },
  "page-not-found": {
    "title": "Página no encontrada",
    "content": "La ruta <strong>{{ invalid_path }}</strong> no es válida.",
    "go-home": "Ir a Inicio"
  },
  "footer": {
    "rights": "Todos los derechos reservados.",
    "powered-by": "Desarrollado con",
    "and": "y"
  }
}
```

---

## PASO 5 — Configuración del JSON-Server

**Crear** la carpeta `server` en la carpeta raíz del proyecto:

```markdown
- 📂 ea20262u<TU-CODIGO>
  - 📁 server
```

**Crear** el archivo `db.json` en la carpeta `server` con el siguiente contenido:

### `server/db.json`

```json
{
  "cellars": [
    { "id": 1, "name": "Reds Cellar",      "wineType": "reds",      "capacity": 500 },
    { "id": 2, "name": "Whites Cellar",    "wineType": "whites",    "capacity": 400 },
    { "id": 3, "name": "Sparkling Cellar", "wineType": "sparkling", "capacity": 300 },
    { "id": 4, "name": "Rosé Cellar",      "wineType": "rose",      "capacity": 250 },
    { "id": 5, "name": "Dessert Cellar",   "wineType": "dessert",   "capacity": 200 },
    { "id": 6, "name": "Port Cellar",      "wineType": "port",      "capacity": 180 }
  ],
  "preservation-items": [
    {
      "id": 1, "cellarId": 1, "wineType": "reds",
      "wineId": 1, "wineName": "Eszencia 1999",
      "quantity": 42, "registeredAt": "2026-05-10T14:30:00.000Z"
    },
    {
      "id": 2, "cellarId": 1, "wineType": "reds",
      "wineId": 12, "wineName": "Vega Sicilia Único",
      "quantity": 18, "registeredAt": "2026-05-12T09:15:00.000Z"
    },
    {
      "id": 3, "cellarId": 2, "wineType": "whites",
      "wineId": 101, "wineName": "Cloudy Bay Sauvignon Blanc",
      "quantity": 35, "registeredAt": "2026-05-13T16:45:00.000Z"
    },
    {
      "id": 4, "cellarId": 3, "wineType": "sparkling",
      "wineId": 201, "wineName": "Moët & Chandon Impérial",
      "quantity": 24, "registeredAt": "2026-05-15T11:20:00.000Z"
    },
    {
      "id": 5, "cellarId": 4, "wineType": "rose",
      "wineId": 301, "wineName": "Domaine Ott Rosé",
      "quantity": 15, "registeredAt": "2026-05-16T08:00:00.000Z"
    },
    {
      "id": 6, "cellarId": 5, "wineType": "dessert",
      "wineId": 501, "wineName": "Château d'Yquem 2015",
      "quantity": 8, "registeredAt": "2026-05-17T10:30:00.000Z"
    }
  ]
}
```

**Cargar** el Terminal del IDE y **agregar** un nuevo Tab.

**Ejecutar** el siguiente command para iniciar el `json-server`:

```bash
json-server --watch server/db.json
```

**Cargar** el navegador e **ingresar** las siguientes URLs:
- http://localhost:3000/cellars
- http://localhost:3000/preservation-items

---

## PASO 6 — Configuración de environments

**Ejecutar** el siguiente CLI command:

```bash
ng generate environments
```

**Agregar** los siguientes valores a la constante `environment` del archivo `environment.development.ts` ubicado en `/src/environments`:

```ts
production: false,
cellarApiBaseUrl: 'http://localhost:3000',
cellarsEndpointPath: '/cellars',
preservationItemsEndpointPath: '/preservation-items',
wineryApiBaseUrl: 'https://api.sampleapis.com/wines',
logoApiBaseUrl: 'https://logo.clearbit.com/'
```

**Agregar** los siguientes valores a la constante `environment` del archivo `environment.ts` ubicado en `/src/environments`:

```ts
production: true,
cellarApiBaseUrl: 'http://localhost:3000',
cellarsEndpointPath: '/cellars',
preservationItemsEndpointPath: '/preservation-items',
wineryApiBaseUrl: 'https://api.sampleapis.com/wines',
logoApiBaseUrl: 'https://logo.clearbit.com/'
```

---

## PASO 7 — Configuración del appConfig

**Agregar** los siguientes imports al archivo `app.config.ts` ubicado en `/src/app`:

```ts
import { provideAppInitializer, inject } from '@angular/core';
import { provideHttpClient } from '@angular/common/http';
import { provideTranslateService, TranslateService } from '@ngx-translate/core';
import { provideTranslateHttpLoader } from '@ngx-translate/http-loader';
```

**Agregar** los siguientes métodos al array `providers` de la constante `appConfig`:

```ts
provideHttpClient(),
provideTranslateService({
  loader: provideTranslateHttpLoader({ prefix: './assets/i18n/', suffix: '.json' }),
  lang: 'en',
  fallbackLang: 'en'
}),
provideAppInitializer(() => {
  const translate = inject(TranslateService);
  translate.use(translate.getBrowserLang() || 'en');
})
```

---

## PASO 8 — Creación de la estructura del proyecto

**Crear** la siguiente estructura de carpetas en `/src/app`:

```markdown
- 📂 src
  - 📂 app
    - 📂 preservation
      - 📁 application
      - 📁 domain
        - 📁 model
      - 📁 infrastructure
      - 📁 presentation
        - 📁 components
        - 📁 views
    - 📂 winery
      - 📁 application
      - 📁 domain
        - 📁 model
      - 📁 infrastructure
      - 📁 presentation
        - 📁 components
        - 📁 views
    - 📂 shared
      - 📁 infrastructure
      - 📁 presentation
        - 📁 components
        - 📁 views
```

---

## PASO 9 — Creación de interfaces y clases Base

**Ejecutar** los siguientes CLI commands:

```bash
ng generate interface shared/infrastructure/base-entity
```
```bash
ng generate interface shared/infrastructure/base-response
```
```bash
ng generate interface shared/infrastructure/base-assembler
```
```bash
ng generate class shared/infrastructure/base-api --skip-tests=true
```
```bash
ng generate class shared/infrastructure/base-api-endpoint --skip-tests=true
```

### `shared/infrastructure/base-entity.ts`

**Reemplazar** el contenido con:

```ts
export interface BaseEntity {
  /**
   * The unique identifier for the entity.
   */
  id: number;
}
```

### `shared/infrastructure/base-response.ts`

**Reemplazar** el contenido con:

```ts
export interface BaseResponse {}

/**
 * Defines a standard structure for API resources/DTOs with a unique identifier.
 */
export interface BaseResource {
  /**
   * The unique identifier for the resource.
   */
  id: number;
}
```

### `shared/infrastructure/base-assembler.ts`

**Reemplazar** el contenido con:

```ts
import { BaseResource, BaseResponse } from './base-response';
import { BaseEntity } from './base-entity';

/**
 * Defines a contract for assembler classes that convert between entities, resources, and API responses.
 *
 * @template TEntity - The entity type, must extend BaseEntity.
 * @template TResource - The resource type, must extend BaseResource.
 * @template TResponse - The response type, must extend BaseResponse.
 */
export interface BaseAssembler<TEntity extends BaseEntity, TResource extends BaseResource, TResponse extends BaseResponse> {
  toEntityFromResource(resource: TResource): TEntity;
  toResourceFromEntity(entity: TEntity): TResource;
  toEntitiesFromResponse(response: TResponse): TEntity[];
}
```

### `shared/infrastructure/base-api.ts`

**Reemplazar** el contenido con:

```ts
/**
 * Abstract base class for API services managing multiple endpoints within a bounded context.
 */
export abstract class BaseApi {
  // No methods defined; child classes will compose endpoint instances
}
```

### `shared/infrastructure/base-api-endpoint.ts`

**Reemplazar** el contenido con:

```ts
import { HttpClient, HttpErrorResponse } from '@angular/common/http';
import { Observable, throwError } from 'rxjs';
import { catchError, map } from 'rxjs/operators';
import { BaseEntity } from './base-entity';
import { BaseResource, BaseResponse } from './base-response';
import { BaseAssembler } from './base-assembler';

/**
 * Base class for API endpoint operations with generic CRUD functionality.
 *
 * @template TEntity - The entity type, must extend BaseEntity.
 * @template TResource - The resource type, must extend BaseResource.
 * @template TResponse - The response type, must extend BaseResponse.
 * @template TAssembler - The assembler type implementing BaseAssembler.
 */
export abstract class BaseApiEndpoint<
  TEntity extends BaseEntity,
  TResource extends BaseResource,
  TResponse extends BaseResponse,
  TAssembler extends BaseAssembler<TEntity, TResource, TResponse>
> {
  constructor(
    protected http: HttpClient,
    protected endpointUrl: string,
    protected assembler: TAssembler
  ) {}

  /**
   * Retrieves all entities from the API, handling both response objects and arrays.
   * @returns An Observable of an array of entities.
   */
  getAll(): Observable<TEntity[]> {
    return this.http.get<TResponse | TResource[]>(this.endpointUrl).pipe(
      map(response => {
        console.log(response);
        if (Array.isArray(response)) {
          return response.map(resource => this.assembler.toEntityFromResource(resource));
        }
        return this.assembler.toEntitiesFromResponse(response as TResponse);
      }),
      catchError(this.handleError('Failed to fetch entities'))
    );
  }

  /**
   * Retrieves a single entity by ID.
   * @param id - The ID of the entity.
   */
  getById(id: number): Observable<TEntity> {
    return this.http.get<TResource>(`${this.endpointUrl}/${id}`).pipe(
      map(resource => this.assembler.toEntityFromResource(resource)),
      catchError(this.handleError('Failed to fetch entity'))
    );
  }

  /**
   * Creates a new entity.
   * @param entity - The entity to create.
   */
  create(entity: TEntity): Observable<TEntity> {
    const resource = this.assembler.toResourceFromEntity(entity);
    return this.http.post<TResource>(this.endpointUrl, resource).pipe(
      map(created => this.assembler.toEntityFromResource(created)),
      catchError(this.handleError('Failed to create entity'))
    );
  }

  /**
   * Updates an existing entity.
   * @param entity - The entity to update.
   * @param id - The ID of the entity.
   */
  update(entity: TEntity, id: number): Observable<TEntity> {
    const resource = this.assembler.toResourceFromEntity(entity);
    return this.http.put<TResource>(`${this.endpointUrl}/${id}`, resource).pipe(
      map(updated => this.assembler.toEntityFromResource(updated)),
      catchError(this.handleError('Failed to update entity'))
    );
  }

  /**
   * Deletes an entity by ID.
   * @param id - The ID of the entity to delete.
   */
  delete(id: number): Observable<void> {
    return this.http.delete<void>(`${this.endpointUrl}/${id}`).pipe(
      catchError(this.handleError('Failed to delete entity'))
    );
  }

  protected handleError(operation: string) {
    return (error: HttpErrorResponse): Observable<never> => {
      let errorMessage = operation;
      if (error.status === 404) {
        errorMessage = `${operation}: Resource not found`;
      } else if (error.error instanceof ErrorEvent) {
        errorMessage = `${operation}: ${error.error.message}`;
      } else {
        errorMessage = `${operation}: ${error.statusText || 'Unexpected error'}`;
      }
      return throwError(() => new Error(errorMessage));
    };
  }
}
```

---

## PASO 10 — Dominio Winery (SampleAPI wines)

### Analizando el endpoint de SampleAPI

Diríjase a `https://api.sampleapis.com/wines/reds` y **evalúe** el json de respuesta:

```json
[
  {
    "winery": "Oremus",
    "wine": "Eszencia 1999",
    "rating": { "average": "5.0", "reviews": "34 ratings" },
    "location": "Hungary\n·\nTokaj",
    "image": "https://images.vivino.com/...",
    "id": 1
  }
]
```

> **Nota:** El campo `wine` del API es el nombre del vino. En la entidad de dominio lo llamamos `name` (convención TypeScript). El Assembler es responsable de esta traducción.

### Creación de la interface Wine tipo Response

**Ejecutar**:

```bash
ng generate interface winery/infrastructure/winery-response
```

**Reemplazar** el contenido del archivo `winery-response.ts` ubicado en `/src/app/winery/infrastructure` con:

```ts
import { BaseResource, BaseResponse } from '../../shared/infrastructure/base-response';

/**
 * Represents the API response structure for a list of wines.
 */
export interface WineryResponse extends BaseResponse {
  wines: WineResource[];
}

/**
 * Represents the API resource/DTO for a wine from SampleAPI.
 * Note: SampleAPI uses 'wine' for the wine name — mapped to 'name' in domain entity by assembler.
 */
export interface WineResource extends BaseResource {
  id: number;
  winery: string;
  wine: string;
  location: string;
  image: string;
  rating: {
    average: string;
    reviews: string;
  };
}
```

### Creación del class Wine tipo entity (model)

**Ejecutar**:

```bash
ng generate class winery/domain/model/wine --type=entity --skip-tests=true
```

**Agregar** el siguiente `import` a la class `Wine` del archivo `wine.entity.ts`:

```ts
import { BaseEntity } from '../../../shared/infrastructure/base-entity';
```

**Agregar** la interface `BaseEntity` a la clase `Wine`:

```ts
export class Wine implements BaseEntity
```

**Agregar** los siguientes atributos y constructor:

```ts
private _id: number;
private _winery: string;
private _name: string;
private _location: string;
private _image: string;

constructor(wine: { id: number; winery: string; name: string; location: string; image: string }) {
  this._id = wine.id;
  this._winery = wine.winery;
  this._name = wine.name;
  this._location = wine.location;
  this._image = wine.image;
}

get id(): number { return this._id; }
set id(value: number) { this._id = value; }

get winery(): string { return this._winery; }
set winery(value: string) { this._winery = value; }

get name(): string { return this._name; }
set name(value: string) { this._name = value; }

get location(): string { return this._location; }
set location(value: string) { this._location = value; }

get image(): string { return this._image; }
set image(value: string) { this._image = value; }
```

### Creación del class WineAssembler tipo Assembler

**Ejecutar**:

```bash
ng generate class winery/infrastructure/wine-assembler --skip-tests=true
```

**Agregar** los siguientes `import` al archivo `wine-assembler.ts`:

```ts
import { BaseAssembler } from '../../shared/infrastructure/base-assembler';
import { Wine } from '../domain/model/wine.entity';
import { WineResource, WineryResponse } from './winery-response';
```

**Agregar** la interface `BaseAssembler` a la clase `WineAssembler`:

```ts
export class WineAssembler implements BaseAssembler<Wine, WineResource, WineryResponse>
```

**Reemplazar** el contenido de la clase con:

```ts
/**
 * Converts a WineryResponse to an array of Wine entities.
 */
toEntitiesFromResponse(response: WineryResponse): Wine[] {
  return response.wines.map(resource => this.toEntityFromResource(resource));
}

/**
 * Converts a WineResource to a Wine entity.
 * Maps the SampleAPI 'wine' field to the domain entity 'name' field.
 */
toEntityFromResource(resource: WineResource): Wine {
  return new Wine({
    id: resource.id,
    winery: resource.winery,
    name: resource.wine,
    location: resource.location,
    image: resource.image
  });
}

/**
 * Converts a Wine entity to a WineResource.
 */
toResourceFromEntity(entity: Wine): WineResource {
  return {
    id: entity.id,
    winery: entity.winery,
    wine: entity.name,
    location: entity.location,
    image: entity.image,
    rating: { average: '', reviews: '' }
  } as WineResource;
}
```

### Creación del class WineryApiEndpoint

**Ejecutar**:

```bash
ng generate class winery/infrastructure/winery-api-endpoint --skip-tests=true
```

**Agregar** los siguientes `import` al archivo `winery-api-endpoint.ts`:

```ts
import { BaseApiEndpoint } from '../../shared/infrastructure/base-api-endpoint';
import { Wine } from '../domain/model/wine.entity';
import { WineResource, WineryResponse } from './winery-response';
import { WineAssembler } from './wine-assembler';
import { HttpClient } from '@angular/common/http';
import { environment } from '../../../environments/environment';
```

**Extends** `BaseApiEndpoint` a la clase `WineryApiEndpoint`:

```ts
export class WineryApiEndpoint extends BaseApiEndpoint<Wine, WineResource, WineryResponse, WineAssembler>
```

**Reemplazar** el contenido de la clase con:

```ts
/**
 * Creates an instance of WineryApiEndpoint.
 * @param http - The HttpClient to use for API requests.
 * @param wineType - The wine type path segment (e.g., 'reds', 'whites').
 */
constructor(http: HttpClient, wineType: string) {
  super(
    http,
    `${environment.wineryApiBaseUrl}/${wineType}`,
    new WineAssembler()
  );
}
```

### Creación del service WineryApi

**Ejecutar**:

```bash
ng generate service winery/infrastructure/winery-api --skip-tests=true
```

**Agregar** los siguientes `import` al archivo `winery-api.service.ts`:

```ts
import { BaseApi } from '../../shared/infrastructure/base-api';
import { Wine } from '../domain/model/wine.entity';
import { HttpClient } from '@angular/common/http';
import { WineryApiEndpoint } from './winery-api-endpoint';
import { Observable } from 'rxjs';
```

**Extends** `BaseApi` a la clase `WineryApi`:

```ts
export class WineryApi extends BaseApi
```

**Reemplazar** el contenido de la clase con:

```ts
constructor(private http: HttpClient) {
  super();
}

/**
 * Retrieves all wines for the given wine type from SampleAPI.
 * @param wineType - The wine type (e.g., 'reds', 'whites', 'sparkling').
 * @returns An Observable of an array of Wine objects.
 */
getWinesByType(wineType: string): Observable<Wine[]> {
  return new WineryApiEndpoint(this.http, wineType).getAll();
}
```

### Creación del service WineryStore

**Ejecutar**:

```bash
ng generate service winery/application/winery-store --skip-tests=true
```

**Agregar** los siguientes `import` al archivo `winery-store.service.ts`:

```ts
import { computed, signal } from '@angular/core';
import { Wine } from '../domain/model/wine.entity';
import { WineryApi } from '../infrastructure/winery-api.service';
```

**Reemplazar** el contenido de la clase `WineryStore` con:

```ts
private readonly winesSignal = signal<Wine[]>([]);
private readonly loadingSignal = signal<boolean>(false);
private readonly errorSignal = signal<string | null>(null);

readonly wines = this.winesSignal.asReadonly();
readonly loading = this.loadingSignal.asReadonly();
readonly error = this.errorSignal.asReadonly();

readonly wineTypes: string[] = ['reds', 'whites', 'sparkling', 'rose', 'dessert', 'port'];

readonly wineCount = computed(() => this.wines().length);

constructor(private wineryApi: WineryApi) {}

/**
 * Loads wines for the given wine type from SampleAPI.
 * @param wineType - The wine type to load.
 */
loadWinesByType(wineType: string): void {
  this.loadingSignal.set(true);
  this.errorSignal.set(null);
  this.winesSignal.set([]);
  this.wineryApi.getWinesByType(wineType).subscribe({
    next: wines => {
      this.winesSignal.set(wines);
      this.loadingSignal.set(false);
    },
    error: err => {
      this.errorSignal.set(this.formatError(err, 'Failed to load wines'));
      this.loadingSignal.set(false);
    }
  });
}

/**
 * Clears the current wine list.
 */
clearWines(): void {
  this.winesSignal.set([]);
}

private formatError(error: any, fallback: string): string {
  if (error instanceof Error) {
    return error.message.includes('Resource not found') ? `${fallback}: Not found` : error.message;
  }
  return fallback;
}
```

---

## PASO 11 — Dominio Preservation (Cellars y PreservationItems)

### Analizando el endpoint cellars

Diríjase a http://localhost:3000/cellars y **evalúe** el json de respuesta:

```json
[
  { "id": 1, "name": "Reds Cellar", "wineType": "reds", "capacity": 500 }
]
```

### Analizando el endpoint preservation-items

Diríjase a http://localhost:3000/preservation-items y **evalúe** el json:

```json
[
  {
    "id": 1, "cellarId": 1, "wineType": "reds",
    "wineId": 1, "wineName": "Eszencia 1999",
    "quantity": 42, "registeredAt": "2026-05-10T14:30:00.000Z"
  }
]
```

### Creación de la interface Cellar tipo Response

**Ejecutar**:

```bash
ng generate interface preservation/infrastructure/cellar-response
```

**Reemplazar** el contenido del archivo `cellar-response.ts` ubicado en `/src/app/preservation/infrastructure` con:

```ts
import { BaseResource, BaseResponse } from '../../shared/infrastructure/base-response';

/**
 * Represents the API response structure for a list of cellars.
 */
export interface CellarsResponse extends BaseResponse {
  cellars: CellarResource[];
}

/**
 * Represents the API resource/DTO for a Cellar.
 */
export interface CellarResource extends BaseResource {
  id: number;
  name: string;
  wineType: string;
  capacity: number;
}
```

### Creación de la interface PreservationItem tipo Response

**Ejecutar**:

```bash
ng generate interface preservation/infrastructure/preservation-item-response
```

**Reemplazar** el contenido del archivo `preservation-item-response.ts` con:

```ts
import { BaseResource, BaseResponse } from '../../shared/infrastructure/base-response';

/**
 * Represents the API response structure for a list of preservation items.
 */
export interface PreservationItemsResponse extends BaseResponse {
  items: PreservationItemResource[];
}

/**
 * Represents the API resource/DTO for a PreservationItem.
 */
export interface PreservationItemResource extends BaseResource {
  id: number;
  cellarId: number;
  wineType: string;
  wineId: number;
  wineName: string;
  quantity: number;
  registeredAt: string;
}
```

### Creación del class Cellar tipo entity (model)

**Ejecutar**:

```bash
ng generate class preservation/domain/model/cellar --type=entity --skip-tests=true
```

**Agregar** el siguiente `import` al archivo `cellar.entity.ts`:

```ts
import { BaseEntity } from '../../../shared/infrastructure/base-entity';
```

**Agregar** `BaseEntity` a la clase:

```ts
export class Cellar implements BaseEntity
```

**Agregar** los atributos y constructor:

```ts
private _id: number;
private _name: string;
private _wineType: string;
private _capacity: number;

constructor(cellar: { id: number; name: string; wineType: string; capacity: number }) {
  this._id = cellar.id;
  this._name = cellar.name;
  this._wineType = cellar.wineType;
  this._capacity = cellar.capacity;
}

get id(): number { return this._id; }
set id(value: number) { this._id = value; }

get name(): string { return this._name; }
set name(value: string) { this._name = value; }

get wineType(): string { return this._wineType; }
set wineType(value: string) { this._wineType = value; }

get capacity(): number { return this._capacity; }
set capacity(value: number) { this._capacity = value; }
```

### Creación del class PreservationItem tipo entity (model)

**Ejecutar**:

```bash
ng generate class preservation/domain/model/preservation-item --type=entity --skip-tests=true
```

**Agregar** el siguiente `import` al archivo `preservation-item.entity.ts`:

```ts
import { BaseEntity } from '../../../shared/infrastructure/base-entity';
```

**Agregar** `BaseEntity` a la clase:

```ts
export class PreservationItem implements BaseEntity
```

**Agregar** los atributos y constructor:

```ts
private _id: number;
private _cellarId: number;
private _wineType: string;
private _wineId: number;
private _wineName: string;
private _quantity: number;
private _registeredAt: string;

constructor(item: {
  id: number;
  cellarId: number;
  wineType: string;
  wineId: number;
  wineName: string;
  quantity: number;
  registeredAt: string;
}) {
  this._id = item.id;
  this._cellarId = item.cellarId;
  this._wineType = item.wineType;
  this._wineId = item.wineId;
  this._wineName = item.wineName;
  this._quantity = item.quantity;
  this._registeredAt = item.registeredAt;
}

get id(): number { return this._id; }
set id(value: number) { this._id = value; }

get cellarId(): number { return this._cellarId; }
set cellarId(value: number) { this._cellarId = value; }

get wineType(): string { return this._wineType; }
set wineType(value: string) { this._wineType = value; }

get wineId(): number { return this._wineId; }
set wineId(value: number) { this._wineId = value; }

get wineName(): string { return this._wineName; }
set wineName(value: string) { this._wineName = value; }

get quantity(): number { return this._quantity; }
set quantity(value: number) { this._quantity = value; }

get registeredAt(): string { return this._registeredAt; }
set registeredAt(value: string) { this._registeredAt = value; }
```

### Creación del class CellarAssembler tipo Assembler

**Ejecutar**:

```bash
ng generate class preservation/infrastructure/cellar-assembler --skip-tests=true
```

**Agregar** los siguientes `import` al archivo `cellar-assembler.ts`:

```ts
import { BaseAssembler } from '../../shared/infrastructure/base-assembler';
import { Cellar } from '../domain/model/cellar.entity';
import { CellarResource, CellarsResponse } from './cellar-response';
```

**Agregar** la interface `BaseAssembler` a la clase:

```ts
export class CellarAssembler implements BaseAssembler<Cellar, CellarResource, CellarsResponse>
```

**Reemplazar** el contenido de la clase con:

```ts
toEntitiesFromResponse(response: CellarsResponse): Cellar[] {
  return response.cellars.map(resource => this.toEntityFromResource(resource));
}

toEntityFromResource(resource: CellarResource): Cellar {
  return new Cellar({
    id: resource.id,
    name: resource.name,
    wineType: resource.wineType,
    capacity: resource.capacity
  });
}

toResourceFromEntity(entity: Cellar): CellarResource {
  return {
    id: entity.id,
    name: entity.name,
    wineType: entity.wineType,
    capacity: entity.capacity
  } as CellarResource;
}
```

### Creación del class PreservationItemAssembler tipo Assembler

**Ejecutar**:

```bash
ng generate class preservation/infrastructure/preservation-item-assembler --skip-tests=true
```

**Agregar** los siguientes `import` al archivo `preservation-item-assembler.ts`:

```ts
import { BaseAssembler } from '../../shared/infrastructure/base-assembler';
import { PreservationItem } from '../domain/model/preservation-item.entity';
import { PreservationItemResource, PreservationItemsResponse } from './preservation-item-response';
```

**Agregar** la interface `BaseAssembler` a la clase:

```ts
export class PreservationItemAssembler implements BaseAssembler<PreservationItem, PreservationItemResource, PreservationItemsResponse>
```

**Reemplazar** el contenido de la clase con:

```ts
toEntitiesFromResponse(response: PreservationItemsResponse): PreservationItem[] {
  return response.items.map(resource => this.toEntityFromResource(resource));
}

toEntityFromResource(resource: PreservationItemResource): PreservationItem {
  return new PreservationItem({
    id: resource.id,
    cellarId: resource.cellarId,
    wineType: resource.wineType,
    wineId: resource.wineId,
    wineName: resource.wineName,
    quantity: resource.quantity,
    registeredAt: resource.registeredAt
  });
}

toResourceFromEntity(entity: PreservationItem): PreservationItemResource {
  return {
    id: entity.id,
    cellarId: entity.cellarId,
    wineType: entity.wineType,
    wineId: entity.wineId,
    wineName: entity.wineName,
    quantity: entity.quantity,
    registeredAt: entity.registeredAt
  } as PreservationItemResource;
}
```

### Creación del class CellarsApiEndpoint

**Ejecutar**:

```bash
ng generate class preservation/infrastructure/cellars-api-endpoint --skip-tests=true
```

**Agregar** los siguientes `import` al archivo `cellars-api-endpoint.ts`:

```ts
import { BaseApiEndpoint } from '../../shared/infrastructure/base-api-endpoint';
import { Cellar } from '../domain/model/cellar.entity';
import { CellarResource, CellarsResponse } from './cellar-response';
import { CellarAssembler } from './cellar-assembler';
import { HttpClient } from '@angular/common/http';
import { environment } from '../../../environments/environment';
```

**Extends** `BaseApiEndpoint` a la clase:

```ts
export class CellarsApiEndpoint extends BaseApiEndpoint<Cellar, CellarResource, CellarsResponse, CellarAssembler>
```

**Reemplazar** el contenido de la clase con:

```ts
constructor(http: HttpClient) {
  super(
    http,
    `${environment.cellarApiBaseUrl}${environment.cellarsEndpointPath}`,
    new CellarAssembler()
  );
}
```

### Creación del class PreservationItemsApiEndpoint

**Ejecutar**:

```bash
ng generate class preservation/infrastructure/preservation-items-api-endpoint --skip-tests=true
```

**Agregar** los siguientes `import` al archivo `preservation-items-api-endpoint.ts`:

```ts
import { BaseApiEndpoint } from '../../shared/infrastructure/base-api-endpoint';
import { PreservationItem } from '../domain/model/preservation-item.entity';
import { PreservationItemResource, PreservationItemsResponse } from './preservation-item-response';
import { PreservationItemAssembler } from './preservation-item-assembler';
import { HttpClient } from '@angular/common/http';
import { environment } from '../../../environments/environment';
```

**Extends** `BaseApiEndpoint` a la clase:

```ts
export class PreservationItemsApiEndpoint extends BaseApiEndpoint<PreservationItem, PreservationItemResource, PreservationItemsResponse, PreservationItemAssembler>
```

**Reemplazar** el contenido de la clase con:

```ts
constructor(http: HttpClient) {
  super(
    http,
    `${environment.cellarApiBaseUrl}${environment.preservationItemsEndpointPath}`,
    new PreservationItemAssembler()
  );
}
```

### Creación del service PreservationApi

**Ejecutar**:

```bash
ng generate service preservation/infrastructure/preservation-api --skip-tests=true
```

**Agregar** los siguientes `import` al archivo `preservation-api.service.ts`:

```ts
import { BaseApi } from '../../shared/infrastructure/base-api';
import { Cellar } from '../domain/model/cellar.entity';
import { PreservationItem } from '../domain/model/preservation-item.entity';
import { HttpClient } from '@angular/common/http';
import { CellarsApiEndpoint } from './cellars-api-endpoint';
import { PreservationItemsApiEndpoint } from './preservation-items-api-endpoint';
import { Observable } from 'rxjs';
```

**Extends** `BaseApi` a la clase:

```ts
export class PreservationApi extends BaseApi
```

**Reemplazar** el contenido de la clase con:

```ts
private readonly cellarsEndpoint: CellarsApiEndpoint;
private readonly preservationItemsEndpoint: PreservationItemsApiEndpoint;

constructor(http: HttpClient) {
  super();
  this.cellarsEndpoint = new CellarsApiEndpoint(http);
  this.preservationItemsEndpoint = new PreservationItemsApiEndpoint(http);
}

/**
 * Retrieves all cellars from the API.
 * @returns An Observable of an array of Cellar objects.
 */
getCellars(): Observable<Cellar[]> {
  return this.cellarsEndpoint.getAll();
}

/**
 * Retrieves all preservation items from the API.
 * @returns An Observable of an array of PreservationItem objects.
 */
getPreservationItems(): Observable<PreservationItem[]> {
  return this.preservationItemsEndpoint.getAll();
}

/**
 * Creates a new preservation item.
 * @param item - The preservation item to create.
 * @returns An Observable of the created PreservationItem.
 */
createPreservationItem(item: PreservationItem): Observable<PreservationItem> {
  return this.preservationItemsEndpoint.create(item);
}
```

---

## PASO 12 — Application Layer: PreservationStore

**Ejecutar**:

```bash
ng generate service preservation/application/preservation-store --skip-tests=true
```

**Agregar** los siguientes `import` al archivo `preservation-store.service.ts` ubicado en `/src/app/preservation/application`:

```ts
import { computed, signal } from '@angular/core';
import { Cellar } from '../domain/model/cellar.entity';
import { PreservationItem } from '../domain/model/preservation-item.entity';
import { PreservationApi } from '../infrastructure/preservation-api.service';
import { takeUntilDestroyed } from '@angular/core/rxjs-interop';
import { retry } from 'rxjs';
```

**Reemplazar** el contenido de la clase `PreservationStore` con:

```ts
private readonly cellarsSignal = signal<Cellar[]>([]);
private readonly preservationItemsSignal = signal<PreservationItem[]>([]);

readonly cellars = this.cellarsSignal.asReadonly();
readonly preservationItems = this.preservationItemsSignal.asReadonly();

private readonly loadingSignal = signal<boolean>(false);
readonly loading = this.loadingSignal.asReadonly();

private readonly errorSignal = signal<string | null>(null);
readonly error = this.errorSignal.asReadonly();

readonly cellarCount = computed(() => this.cellars().length);

constructor(private preservationApi: PreservationApi) {
  this.loadCellars();
  this.loadPreservationItems();
}

/**
 * Returns total bottles for a given cellar.
 * @param cellarId - The cellar ID.
 */
getTotalBottles(cellarId: number): number {
  return this.preservationItems()
    .filter(item => item.cellarId === cellarId)
    .reduce((sum, item) => sum + item.quantity, 0);
}

/**
 * Returns available capacity for a given cellar.
 * @param cellarId - The cellar ID.
 */
getAvailableCapacity(cellarId: number): number {
  const cellar = this.cellars().find(c => c.id === cellarId);
  if (!cellar) return 0;
  return cellar.capacity - this.getTotalBottles(cellarId);
}

/**
 * Returns preservation items for a specific cellar.
 * @param cellarId - The cellar ID.
 */
getItemsByCellar(cellarId: number): PreservationItem[] {
  return this.preservationItems().filter(item => item.cellarId === cellarId);
}

/**
 * Returns the cellar associated with the given wine type.
 * @param wineType - The wine type string.
 */
getCellarByWineType(wineType: string): Cellar | undefined {
  return this.cellars().find(c => c.wineType === wineType);
}

/**
 * Adds a new preservation item.
 * @param item - The preservation item to add.
 */
addPreservationItem(item: PreservationItem): void {
  this.loadingSignal.set(true);
  this.errorSignal.set(null);
  this.preservationApi.createPreservationItem(item).pipe(retry(2)).subscribe({
    next: created => {
      this.preservationItemsSignal.update(items => [...items, created]);
      this.loadingSignal.set(false);
    },
    error: err => {
      this.errorSignal.set(this.formatError(err, 'Failed to create preservation item'));
      this.loadingSignal.set(false);
    }
  });
}

private loadCellars(): void {
  this.loadingSignal.set(true);
  this.errorSignal.set(null);
  this.preservationApi.getCellars().pipe(takeUntilDestroyed()).subscribe({
    next: cellars => {
      this.cellarsSignal.set(cellars);
      this.loadingSignal.set(false);
    },
    error: err => {
      this.errorSignal.set(this.formatError(err, 'Failed to load cellars'));
      this.loadingSignal.set(false);
    }
  });
}

private loadPreservationItems(): void {
  this.loadingSignal.set(true);
  this.errorSignal.set(null);
  this.preservationApi.getPreservationItems().pipe(takeUntilDestroyed()).subscribe({
    next: items => {
      this.preservationItemsSignal.set(items);
      this.loadingSignal.set(false);
    },
    error: err => {
      this.errorSignal.set(this.formatError(err, 'Failed to load preservation items'));
      this.loadingSignal.set(false);
    }
  });
}

private formatError(error: any, fallback: string): string {
  if (error instanceof Error) {
    return error.message.includes('Resource not found') ? `${fallback}: Not found` : error.message;
  }
  return fallback;
}
```

---

## PASO 13 — Creación de Componentes y Vistas

**Cargar** el Terminal del IDE y **agregar** un nuevo Tab.

**Ejecutar** los siguientes commands:

```bash
ng generate component shared/presentation/components/language-switcher --skip-tests=true
```
```bash
ng generate component shared/presentation/components/layout --skip-tests=true
```
```bash
ng generate component shared/presentation/views/home --skip-tests=true
```
```bash
ng generate component shared/presentation/views/page-not-found --skip-tests=true
```
```bash
ng generate component preservation/presentation/components/cellar-summary --skip-tests=true
```
```bash
ng generate component preservation/presentation/views/new-preservation-item --skip-tests=true
```

---

## PASO 14 — Configuración de Routes

### Crear `preservation/presentation/views/preservation.routes.ts`

**Crear** el archivo manualmente con el siguiente contenido:

```ts
import { Routes } from '@angular/router';

const newPreservationItem = () =>
  import('./new-preservation-item/new-preservation-item').then(m => m.NewPreservationItem);

export const preservationRoutes: Routes = [
  { path: 'items/new', loadComponent: newPreservationItem, title: 'The Wine Square - New Preservation Item' }
];
```

### Configurar `src/app/app.routes.ts`

**Agregar** el siguiente `import`:

```ts
import { Home } from './shared/presentation/views/home/home';
```

**Agregar** los siguientes `const` después de los imports y antes de la constante `routes`:

```ts
const pageNotFound = () =>
  import('./shared/presentation/views/page-not-found/page-not-found').then(m => m.PageNotFound);

const baseTitle = 'The Wine Square';
```

**Agregar** los siguientes valores a la constante `routes`:

```ts
{ path: 'home', component: Home, title: `${baseTitle} - Home` },
{
  path: 'preservation',
  loadChildren: () =>
    import('./preservation/presentation/views/preservation.routes').then(m => m.preservationRoutes)
},
{ path: '', redirectTo: '/home', pathMatch: 'full' },
{ path: '**', loadComponent: pageNotFound, title: `${baseTitle} - Page Not Found` }
```

---

## PASO 15 — Modificación del LanguageSwitcher Component

**Agregar** los siguientes `import` al archivo `language-switcher.ts` ubicado en `/src/app/shared/presentation/components/language-switcher`:

```ts
import { inject } from '@angular/core';
import { MatButtonToggle, MatButtonToggleGroup } from '@angular/material/button-toggle';
import { TranslateService } from '@ngx-translate/core';
```

**Agregar** las siguientes clases en el array `imports` del `@Component`:

```
MatButtonToggleGroup, MatButtonToggle
```

**Reemplazar** el contenido de la clase `LanguageSwitcher` con:

```ts
protected currentLang: string = 'en';
protected languages: string[] = ['en', 'es'];
private translate: TranslateService;

constructor() {
  this.translate = inject(TranslateService);
  this.currentLang = this.translate.getCurrentLang();
}

useLanguage(language: string): void {
  this.translate.use(language);
  this.currentLang = language;
}
```

**Reemplazar** el contenido del archivo `language-switcher.html` con:

```html
<mat-button-toggle-group [value]="currentLang"
                         appearance="standard"
                         aria-label="Preferred language"
                         name="language">
  @for (language of languages; track language) {
    <mat-button-toggle [value]="language"
                       [attr.aria-label]="language"
                       (click)="useLanguage(language)">
      {{ language.toUpperCase() }}
    </mat-button-toggle>
  }
</mat-button-toggle-group>
```

---

## PASO 16 — Modificación del Layout Component

**Agregar** los siguientes `import` al archivo `layout.ts` ubicado en `/src/app/shared/presentation/components/layout`:

```ts
import { RouterLink, RouterLinkActive, RouterOutlet } from '@angular/router';
import { MatToolbar, MatToolbarRow } from '@angular/material/toolbar';
import { MatButton } from '@angular/material/button';
import { TranslatePipe } from '@ngx-translate/core';
import { LanguageSwitcher } from '../language-switcher/language-switcher';
import { environment } from '../../../../../environments/environment';
```

**Agregar** las siguientes clases en el array `imports` del `@Component`:

```
RouterOutlet, RouterLink, RouterLinkActive, MatToolbarRow, MatToolbar, MatButton, TranslatePipe, LanguageSwitcher
```

**Reemplazar** el contenido de la clase `Layout` con:

```ts
protected logoUrl = `${environment.logoApiBaseUrl}thewinesquare.com`;

options = [
  { link: '/home', label: 'option.home' },
  { link: '/preservation/items/new', label: 'option.new-preservation-item' }
];
```

**Reemplazar** el contenido del archivo `layout.html` con:

```html
<mat-toolbar role="banner" aria-label="Main navigation">
  <mat-toolbar-row>
    <img [src]="logoUrl" alt="The Wine Square logo" height="36" aria-hidden="true" />
    <span style="margin-left: 10px;">{{ 'toolbar.title' | translate }}</span>
    <div class="mat-spacer"></div>
    @for (option of options; track option.label) {
      <a mat-button
         [routerLink]="option.link"
         routerLinkActive="active-link"
         [attr.aria-label]="option.label | translate">
        {{ option.label | translate }}
      </a>
    }
    <app-language-switcher />
  </mat-toolbar-row>
</mat-toolbar>
<router-outlet />
```

**Reemplazar** el contenido del archivo `layout.css` con:

```css
.mat-spacer {
  flex: 1 1 auto;
}

.active-link {
  font-weight: bold;
  border-bottom: 2px solid white;
}
```

---

## PASO 17 — Modificación del CellarSummary Component

**Agregar** los siguientes `import` al archivo `cellar-summary.ts` ubicado en `/src/app/preservation/presentation/components/cellar-summary`:

```ts
import { Component, Input, inject } from '@angular/core';
import { MatCardModule } from '@angular/material/card';
import { TranslatePipe } from '@ngx-translate/core';
import { Cellar } from '../../../domain/model/cellar.entity';
import { PreservationItem } from '../../../domain/model/preservation-item.entity';
import { PreservationStore } from '../../../application/preservation-store.service';
```

**Agregar** las siguientes clases en el array `imports` del `@Component`:

```
MatCardModule, TranslatePipe
```

**Reemplazar** el contenido de la clase `CellarSummary` con:

```ts
@Input() cellar!: Cellar;

readonly store = inject(PreservationStore);

get items(): PreservationItem[] {
  return this.store.getItemsByCellar(this.cellar.id);
}

get totalBottles(): number {
  return this.store.getTotalBottles(this.cellar.id);
}

get availableCapacity(): number {
  return this.store.getAvailableCapacity(this.cellar.id);
}

get isEmpty(): boolean {
  return this.items.length === 0;
}
```

**Reemplazar** el contenido del archivo `cellar-summary.html` con:

```html
<mat-card role="article" [attr.aria-label]="cellar.name + ' cellar summary'">
  <mat-card-header>
    <mat-card-title>{{ cellar.name }}</mat-card-title>
    <mat-card-subtitle>{{ cellar.wineType }}</mat-card-subtitle>
  </mat-card-header>

  <mat-card-content>
    @if (isEmpty) {
      <p aria-live="polite">{{ 'home.empty' | translate }}</p>
    } @else {
      <ul aria-label="Wines in cellar" style="list-style: none; padding: 0; margin: 0;">
        @for (item of items; track item.id) {
          <li>{{ item.wineName }} — {{ item.quantity }}</li>
        }
      </ul>
    }
  </mat-card-content>

  <mat-card-footer>
    <p><strong>{{ 'home.total-bottles' | translate }}:</strong> {{ totalBottles }}</p>
    <p><strong>{{ 'home.available-capacity' | translate }}:</strong> {{ availableCapacity }}</p>
  </mat-card-footer>
</mat-card>
```

**Reemplazar** el contenido del archivo `cellar-summary.css` con:

```css
mat-card {
  width: 100%;
  margin: 8px;
}

mat-card-footer {
  padding: 8px 16px;
}
```

---

## PASO 18 — Modificación del Home Component

**Agregar** los siguientes `import` al archivo `home.ts` ubicado en `/src/app/shared/presentation/views/home`:

```ts
import { inject } from '@angular/core';
import { MatGridListModule } from '@angular/material/grid-list';
import { TranslatePipe } from '@ngx-translate/core';
import { MatProgressSpinner } from '@angular/material/progress-spinner';
import { MatError } from '@angular/material/form-field';
import { PreservationStore } from '../../../../preservation/application/preservation-store.service';
import { CellarSummary } from '../../../../preservation/presentation/components/cellar-summary/cellar-summary';
```

**Agregar** las siguientes clases en el array `imports` del `@Component`:

```
MatGridListModule, TranslatePipe, MatProgressSpinner, MatError, CellarSummary
```

**Reemplazar** el contenido de la clase `Home` con:

```ts
readonly store = inject(PreservationStore);
```

**Reemplazar** el contenido del archivo `home.html` con:

```html
<section aria-labelledby="home-title">
  <h1 id="home-title">{{ 'home.title' | translate }}</h1>
  <p>{{ 'home.content' | translate }}</p>

  <h2>{{ 'home.my-wine-cellars' | translate }}</h2>

  @if (store.loading()) {
    <mat-spinner diameter="40"></mat-spinner>
  }
  @if (store.error()) {
    <mat-error role="alert">{{ store.error() }}</mat-error>
  }

  <mat-grid-list cols="2" rowHeight="350px" gutterSize="16px" aria-label="Wine cellars grid">
    @for (cellar of store.cellars(); track cellar.id) {
      <mat-grid-tile>
        <app-cellar-summary [cellar]="cellar" />
      </mat-grid-tile>
    }
  </mat-grid-list>
</section>
```

**Reemplazar** el contenido del archivo `home.css` con:

```css
section {
  max-width: 1200px;
  margin: 24px auto;
  padding: 0 16px;
}

h1 {
  margin-bottom: 4px;
}

h2 {
  margin-top: 32px;
  margin-bottom: 16px;
}
```

---

## PASO 19 — Modificación del NewPreservationItem Component

**Agregar** los siguientes `import` al archivo `new-preservation-item.ts` ubicado en `/src/app/preservation/presentation/views/new-preservation-item`:

```ts
import { inject } from '@angular/core';
import { FormBuilder, FormControl, ReactiveFormsModule, Validators } from '@angular/forms';
import { Router } from '@angular/router';
import { MatFormFieldModule } from '@angular/material/form-field';
import { MatSelectModule } from '@angular/material/select';
import { MatInputModule } from '@angular/material/input';
import { MatButtonModule } from '@angular/material/button';
import { TranslatePipe } from '@ngx-translate/core';
import { PreservationStore } from '../../../application/preservation-store.service';
import { WineryStore } from '../../../../winery/application/winery-store.service';
import { PreservationItem } from '../../../domain/model/preservation-item.entity';
```

**Agregar** las siguientes clases en el array `imports` del `@Component`:

```
ReactiveFormsModule, MatFormFieldModule, MatSelectModule, MatInputModule, MatButtonModule, TranslatePipe
```

**Reemplazar** el contenido de la clase `NewPreservationItem` con:

```ts
private fb = inject(FormBuilder);
private router = inject(Router);
readonly store = inject(PreservationStore);
readonly wineryStore = inject(WineryStore);

form = this.fb.group({
  wineType: new FormControl<string>('', { nonNullable: true, validators: [Validators.required] }),
  wineId: new FormControl<number | null>(null, [Validators.required]),
  wineName: new FormControl<string>('', { nonNullable: true }),
  quantity: new FormControl<number | null>(null, [Validators.required, Validators.min(1)])
});

get availableCapacity(): number {
  const wineType = this.form.value.wineType;
  if (!wineType) return 0;
  const cellar = this.store.getCellarByWineType(wineType);
  return cellar ? this.store.getAvailableCapacity(cellar.id) : 0;
}

onWineTypeChange(wineType: string): void {
  this.form.patchValue({ wineId: null, wineName: '', quantity: null });
  this.wineryStore.loadWinesByType(wineType);
}

onWineChange(wineId: number): void {
  const wine = this.wineryStore.wines().find(w => w.id === wineId);
  if (wine) {
    this.form.patchValue({ wineName: wine.name });
  }
}

isQuantityValid(): boolean {
  const qty = this.form.value.quantity;
  return qty !== null && qty !== undefined && qty > 0 && qty <= this.availableCapacity;
}

submit(): void {
  if (this.form.invalid || !this.isQuantityValid()) return;

  const wineType = this.form.value.wineType!;
  const cellar = this.store.getCellarByWineType(wineType);
  if (!cellar) return;

  const item = new PreservationItem({
    id: 0,
    cellarId: cellar.id,
    wineType: wineType,
    wineId: this.form.value.wineId!,
    wineName: this.form.value.wineName!,
    quantity: this.form.value.quantity!,
    registeredAt: new Date().toISOString()
  });

  this.store.addPreservationItem(item);
  this.router.navigate(['/home']).then();
}

cancel(): void {
  this.router.navigate(['/home']).then();
}
```

**Reemplazar** el contenido del archivo `new-preservation-item.html` con:

```html
<section aria-labelledby="form-title">
  <h1 id="form-title">{{ 'preservation.title' | translate }}</h1>
  <h2>{{ 'preservation.subtitle' | translate }}</h2>

  <form [formGroup]="form" (ngSubmit)="submit()" aria-label="New preservation item form">

    <mat-form-field appearance="outline">
      <mat-label>{{ 'preservation.wine-type' | translate }}</mat-label>
      <mat-select formControlName="wineType"
                  (selectionChange)="onWineTypeChange($event.value)"
                  aria-required="true">
        @for (type of wineryStore.wineTypes; track type) {
          <mat-option [value]="type">{{ type }}</mat-option>
        }
      </mat-select>
      @if (form.get('wineType')!.touched && form.get('wineType')!.hasError('required')) {
        <mat-error>{{ 'preservation.wine-type-required' | translate }}</mat-error>
      }
    </mat-form-field>

    <mat-form-field appearance="outline">
      <mat-label>{{ 'preservation.wine' | translate }}</mat-label>
      <mat-select formControlName="wineId"
                  (selectionChange)="onWineChange($event.value)"
                  aria-required="true">
        @if (wineryStore.loading()) {
          <mat-option [value]="null" disabled>Loading wines...</mat-option>
        }
        @for (wine of wineryStore.wines(); track wine.id) {
          <mat-option [value]="wine.id">{{ wine.name }}</mat-option>
        }
      </mat-select>
      @if (form.get('wineId')!.touched && form.get('wineId')!.hasError('required')) {
        <mat-error>{{ 'preservation.wine-required' | translate }}</mat-error>
      }
    </mat-form-field>

    <mat-form-field appearance="outline">
      <mat-label>{{ 'preservation.quantity' | translate }}</mat-label>
      <input matInput
             type="number"
             formControlName="quantity"
             [max]="availableCapacity"
             min="1"
             aria-required="true"
             aria-describedby="capacity-hint" />
      <mat-hint id="capacity-hint">{{ 'home.available-capacity' | translate }}: {{ availableCapacity }}</mat-hint>
      @if (form.get('quantity')!.touched && form.get('quantity')!.hasError('required')) {
        <mat-error>{{ 'preservation.quantity-required' | translate }}</mat-error>
      }
      @if (form.get('quantity')!.value && !isQuantityValid()) {
        <mat-error>{{ 'preservation.quantity-exceeded' | translate }}</mat-error>
      }
    </mat-form-field>

    <div class="form-actions">
      <button mat-raised-button
              color="primary"
              type="submit"
              [disabled]="form.invalid || !isQuantityValid()"
              aria-label="Create preservation item">
        {{ 'preservation.create' | translate }}
      </button>
      <button mat-stroked-button
              type="button"
              (click)="cancel()"
              aria-label="Cancel and return to home">
        {{ 'preservation.cancel' | translate }}
      </button>
    </div>
  </form>
</section>
```

**Reemplazar** el contenido del archivo `new-preservation-item.css` con:

```css
section {
  max-width: 600px;
  margin: 24px auto;
  padding: 0 16px;
}

form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

mat-form-field {
  width: 100%;
}

.form-actions {
  display: flex;
  gap: 12px;
}
```

---

## PASO 20 — Modificación del PageNotFound Component

**Agregar** los siguientes `import` al archivo `page-not-found.ts` ubicado en `/src/app/shared/presentation/views/page-not-found`:

```ts
import { inject } from '@angular/core';
import { Router, RouterLink } from '@angular/router';
import { MatButtonModule } from '@angular/material/button';
import { TranslatePipe } from '@ngx-translate/core';
```

**Agregar** las siguientes clases en el array `imports` del `@Component`:

```
MatButtonModule, RouterLink, TranslatePipe
```

**Reemplazar** el contenido de la clase `PageNotFound` con:

```ts
private router = inject(Router);
protected invalidPath: string = this.router.url;
```

**Reemplazar** el contenido del archivo `page-not-found.html` con:

```html
<section aria-labelledby="not-found-title" style="text-align: center; margin-top: 80px;">
  <h1 id="not-found-title">{{ 'page-not-found.title' | translate }}</h1>
  <p [innerHTML]="'page-not-found.content' | translate: { invalid_path: invalidPath }"></p>
  <a mat-raised-button color="primary" routerLink="/home" aria-label="Go back to home">
    {{ 'page-not-found.go-home' | translate }}
  </a>
</section>
```

---

## PASO 21 — Modificación del App

**Eliminar** el import de `RouterOutlet` del archivo `app.ts` ubicado en `/src/app`.

**Agregar** el siguiente `import` al archivo `app.ts`:

```ts
import { Layout } from './shared/presentation/components/layout/layout';
```

**Eliminar** `RouterOutlet` del array `imports` del `@Component` y **agregar**:

```
Layout
```

**Reemplazar** el contenido del archivo `app.html` con:

```html
<app-layout />
```

---

## PASO 22 — Estilos globales

**Reemplazar** el contenido del archivo `src/styles.css`:

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Roboto, 'Helvetica Neue', sans-serif;
}

mat-grid-tile {
  overflow: visible !important;
}

app-cellar-summary {
  width: 100%;
  height: 100%;
}
```

---

## PASO 23 — README.md

**Crear/reemplazar** el archivo `README.md` en la raíz del proyecto:

```markdown
# The Wine Square — Cellar Management Platform

## Description
A frontend web application built for **The Wine Square**, allowing clients to manage their Wine Cellars and register Preservation Items.

## Features
- View all Wine Cellars with their current wine inventory (grid list 2 columns)
- Cellar Summary cards showing wine name, quantity, Total Bottles and Available Capacity
- Add new Preservation Items (wine bottles) to a cellar
- Dynamic wine selection by wine type via SampleAPI (https://api.sampleapis.com/wines)
- Automatic cellar assignment based on wine type
- Capacity validation before adding items
- Multilingual support: English (default) and Spanish
- Page not found view for invalid routes
- ARIA attributes for accessibility

## Tech Stack
- **Angular** v21+ (Standalone Components, Signals, Router, Child Routes)
- **Angular Material** (UI components: Grid List, Cards, Toolbar, Forms)
- **@ngx-translate/core** (i18n)
- **JSON Server** v0.17.4 (mock backend)
- **TypeScript** (OOP with patterns: Assembler, Api, Endpoint, Store)
- **HttpClient** (@angular/common/http)

## Project Structure
Domain-driven layered architecture with bounded contexts:
- `preservation` — Cellars and Preservation Items
- `winery` — Wine information from SampleAPI
- `shared` — Base classes, interfaces, and shared UI components

## Configuration

### Prerequisites
- Node.js 20+
- Angular CLI 21+
- JSON Server 0.17.4 (`npm install -g json-server@0.17.4`)

### Running the mock backend
```bash
json-server --watch server/db.json
```

### Running the app
```bash
ng serve --port 4200
```

Access at: `http://localhost:4200`

## Author
**Tu Nombre y Apellido**
Student Code: `<TU-CODIGO>`
Course: Desarrollo de Aplicaciones Open Source (1ASI0729) — NRC 20262
Universidad Peruana de Ciencias Aplicadas (UPC)
```

---

## PASO 24 — Verificación final antes de entregar

1. Verifica que `json-server` esté corriendo y los endpoints respondan:
   - http://localhost:3000/cellars
   - http://localhost:3000/preservation-items

2. Ejecuta la app sin errores:
   ```bash
   ng serve --port 4200
   ```

3. Verifica las rutas:
   - `/` → redirige a `/home`
   - `/home` → vista Home con grid de cellars
   - `/preservation/items/new` → formulario New Preservation Item
   - Cualquier ruta inválida → vista Page Not Found

4. **Elimina** la carpeta `node_modules`:
   ```bash
   rm -rf node_modules
   ```

5. Genera el ZIP con nombre correcto:
   ```bash
   zip -r ea20262u<TU-CODIGO>.zip . -x "*.git*"
   ```

> **Importante:** Reemplaza `Tu Nombre y Apellido` y `<TU-CODIGO>` con tus datos reales en todos los archivos.
