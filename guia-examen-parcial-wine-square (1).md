# Guía Paso a Paso — Examen Parcial: The Wine Square
### Curso: Desarrollo de Aplicaciones Open Source (1ASI0729) | NRC: 20262

---

## PASO 1 — Creación del Proyecto Angular

Abre el **Terminal** del sistema operativo, ubícate en tu carpeta de preferencia y ejecuta:

```bash
ng new ea20262u<TU-CODIGO>
```

> Reemplaza `<TU-CODIGO>` con tu código de estudiante en minúsculas. Ejemplo: `ea20262u202112345`

Selecciona las siguientes opciones:

**¿Formato de stylesheet?**
```
CSS
```

**¿Habilitar SSR/SSG?**
```
N
```

**¿Aplicación zoneless?**
```
Y
```

**¿Herramientas AI?** Selecciona ambas con `<space>`:
```
(*) GitHub Copilot
(*) JetBrains AI Assistant
```

---

## PASO 2 — Instalar Angular Material

```bash
cd ea20262u<TU-CODIGO>
```

```bash
ng add @angular/material
```

Opciones a seleccionar:

**¿Proceder con la instalación?**
```
Y
```

**¿Tema prebuilt?** Selecciona el más cercano al estilo de The Wine Square (tonos cálidos/oscuros):
```
Rose/Red   [Preview: https://material.angular.io?theme=rose-red]
```

> Si no existe `Rose/Red`, elige `Deep Purple/Amber` o `Custom` para aplicar colores de vino manualmente.

---

## PASO 3 — Instalar dependencias adicionales

```bash
npm install @ngx-translate/core @ngx-translate/http-loader --save
```

```bash
npm install -g json-server@0.17.4
```

---

## PASO 4 — Archivos de idioma (i18n)

**Crear** las carpetas en `public/`:

```
public/
  assets/
    i18n/
```

### `public/assets/i18n/en.json`

```json
{
  "toolbar": {
    "title": "The Wine Square Cellar Management Platform"
  },
  "nav": {
    "home": "Home",
    "new-preservation-item": "New Preservation Item"
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
    "title": "Page Not Found",
    "content": "The path <strong>{{ path }}</strong> was not found.",
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
  "toolbar": {
    "title": "The Wine Square Plataforma de Gestión de Bodegas"
  },
  "nav": {
    "home": "Inicio",
    "new-preservation-item": "Nuevo Item de Preservación"
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
    "title": "Página No Encontrada",
    "content": "La ruta <strong>{{ path }}</strong> no fue encontrada.",
    "go-home": "Ir al Inicio"
  },
  "footer": {
    "rights": "Todos los derechos reservados.",
    "powered-by": "Desarrollado con",
    "and": "y"
  }
}
```

---

## PASO 5 — Configuración del JSON-Server (db.json)

**Crear** la carpeta `server/` en la raíz del proyecto y dentro crear el archivo `db.json` con el siguiente contenido:

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

La estructura quedará:
```
server/
  db.json
```

Para iniciar el servidor (en terminal separado):

```bash
cd server
json-server --watch db.json
```

Endpoints disponibles:
- `http://localhost:3000/cellars`
- `http://localhost:3000/preservation-items`

> **Importante:** json-server convierte automáticamente la clave `preservation-items` del JSON al endpoint `/preservation-items`.

---

## PASO 6 — Configuración de Environments

```bash
ng generate environments
```

### `src/environments/environment.development.ts`

```ts
export const environment = {
  production: false,
  cellarApiBaseUrl: 'http://localhost:3000',
  cellarsEndpointPath: '/cellars',
  preservationItemsEndpointPath: '/preservation-items',
  wineryApiBaseUrl: 'https://api.sampleapis.com/wines',
  logoApiBaseUrl: 'https://img.logo.dev'
};
```

### `src/environments/environment.ts`

```ts
export const environment = {
  production: true,
  cellarApiBaseUrl: 'http://localhost:3000',
  cellarsEndpointPath: '/cellars',
  preservationItemsEndpointPath: '/preservation-items',
  wineryApiBaseUrl: 'https://api.sampleapis.com/wines',
  logoApiBaseUrl: 'https://img.logo.dev'
};
```

> **Nota:** El path `/preservation-items` (con guión) coincide exactamente con la clave del `db.json`, que json-server expone como `http://localhost:3000/preservation-items`.

---

## PASO 7 — Configuración del `app.config.ts`

**Reemplazar** el contenido de `src/app/app.config.ts`:

```ts
import { ApplicationConfig, provideAppInitializer, inject } from '@angular/core';
import { provideRouter } from '@angular/router';
import { routes } from './app.routes';
import { provideHttpClient } from '@angular/common/http';
import { provideTranslateService, TranslateService } from '@ngx-translate/core';
import { provideTranslateHttpLoader } from '@ngx-translate/http-loader';
import { provideAnimationsAsync } from '@angular/platform-browser/animations/async';

export const appConfig: ApplicationConfig = {
  providers: [
    provideRouter(routes),
    provideAnimationsAsync(),
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
  ]
};
```

---

## PASO 8 — Estructura de carpetas del proyecto

Crear la siguiente estructura dentro de `src/app/`:

```
src/app/
  shared/
    infrastructure/
    presentation/
      components/
      views/
  preservation/
    domain/
      model/
    application/
    infrastructure/
    presentation/
      components/
      views/
  winery/
    domain/
      model/
    application/
    infrastructure/
    presentation/
      components/
      views/
```

---

## PASO 9 — Interfaces y clases base (shared/infrastructure)

### Generar archivos base

```bash
ng generate interface shared/infrastructure/base-entity
ng generate interface shared/infrastructure/base-response
ng generate interface shared/infrastructure/base-assembler
ng generate class shared/infrastructure/base-api --skip-tests=true
ng generate class shared/infrastructure/base-api-endpoint --skip-tests=true
```

### `base-entity.ts`

```ts
/**
 * @summary Base interface for all domain entities.
 * @author Tu Nombre y Apellido
 */
export interface BaseEntity {
  /** The unique identifier for the entity. */
  id: number;
}
```

### `base-response.ts`

```ts
/**
 * @summary Base interface for API responses.
 * @author Tu Nombre y Apellido
 */
export interface BaseResponse {}

/**
 * @summary Base interface for API resources/DTOs with a unique identifier.
 */
export interface BaseResource {
  /** The unique identifier for the resource. */
  id: number;
}
```

### `base-assembler.ts`

```ts
import { BaseResource, BaseResponse } from './base-response';
import { BaseEntity } from './base-entity';

/**
 * @summary Defines a contract for assembler classes that convert between entities, resources, and API responses.
 * @author Tu Nombre y Apellido
 */
export interface BaseAssembler<
  TEntity extends BaseEntity,
  TResource extends BaseResource,
  TResponse extends BaseResponse
> {
  toEntityFromResource(resource: TResource): TEntity;
  toResourceFromEntity(entity: TEntity): TResource;
  toEntitiesFromResponse(response: TResponse): TEntity[];
}
```

### `base-api.ts`

```ts
/**
 * @summary Abstract base class for API services managing multiple endpoints within a bounded context.
 * @author Tu Nombre y Apellido
 */
export abstract class BaseApi {
  // Child classes compose endpoint instances
}
```

### `base-api-endpoint.ts`

```ts
import { HttpClient, HttpErrorResponse } from '@angular/common/http';
import { Observable, throwError } from 'rxjs';
import { catchError, map } from 'rxjs/operators';
import { BaseEntity } from './base-entity';
import { BaseResource, BaseResponse } from './base-response';
import { BaseAssembler } from './base-assembler';

/**
 * @summary Base class for API endpoint operations with generic CRUD functionality.
 * @author Tu Nombre y Apellido
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

  /** Retrieves all entities from the API. */
  getAll(): Observable<TEntity[]> {
    return this.http.get<TResponse | TResource[]>(this.endpointUrl).pipe(
      map(response => {
        if (Array.isArray(response)) {
          return response.map(resource => this.assembler.toEntityFromResource(resource));
        }
        return this.assembler.toEntitiesFromResponse(response as TResponse);
      }),
      catchError(this.handleError('Failed to fetch entities'))
    );
  }

  /** Retrieves a single entity by ID. */
  getById(id: number): Observable<TEntity> {
    return this.http.get<TResource>(`${this.endpointUrl}/${id}`).pipe(
      map(resource => this.assembler.toEntityFromResource(resource)),
      catchError(this.handleError('Failed to fetch entity'))
    );
  }

  /** Creates a new entity. */
  create(entity: TEntity): Observable<TEntity> {
    const resource = this.assembler.toResourceFromEntity(entity);
    return this.http.post<TResource>(this.endpointUrl, resource).pipe(
      map(created => this.assembler.toEntityFromResource(created)),
      catchError(this.handleError('Failed to create entity'))
    );
  }

  /** Updates an existing entity. */
  update(entity: TEntity, id: number): Observable<TEntity> {
    const resource = this.assembler.toResourceFromEntity(entity);
    return this.http.put<TResource>(`${this.endpointUrl}/${id}`, resource).pipe(
      map(updated => this.assembler.toEntityFromResource(updated)),
      catchError(this.handleError('Failed to update entity'))
    );
  }

  /** Deletes an entity by ID. */
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

## PASO 10 — Dominio Winery (SampleAPI)

### Generar archivos

```bash
ng generate interface winery/infrastructure/winery-response
ng generate class winery/domain/model/wine --type=entity --skip-tests=true
ng generate class winery/infrastructure/wine-assembler --skip-tests=true
ng generate class winery/infrastructure/winery-api-endpoint --skip-tests=true
ng generate service winery/infrastructure/winery-api --skip-tests=true
ng generate service winery/application/winery-store --skip-tests=true
```

### `winery/infrastructure/winery-response.ts`

```ts
import { BaseResource, BaseResponse } from '../../shared/infrastructure/base-response';

/**
 * @summary Response structure for the Winery SampleAPI.
 * @author Tu Nombre y Apellido
 */
export interface WineryResponse extends BaseResponse {
  wines: WineResource[];
}

/**
 * @summary Resource/DTO for a Wine object from SampleAPI.
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

### `winery/domain/model/wine.entity.ts`

```ts
import { BaseEntity } from '../../../shared/infrastructure/base-entity';

/**
 * @summary Domain entity representing a Wine from the Winery API.
 * @author Tu Nombre y Apellido
 */
export class Wine implements BaseEntity {
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
}
```

### `winery/infrastructure/wine-assembler.ts`

```ts
import { BaseAssembler } from '../../shared/infrastructure/base-assembler';
import { Wine } from '../domain/model/wine.entity';
import { WineResource, WineryResponse } from './winery-response';

/**
 * @summary Assembler that converts between WineResource and Wine entity.
 * @author Tu Nombre y Apellido
 */
export class WineAssembler implements BaseAssembler<Wine, WineResource, WineryResponse> {

  toEntitiesFromResponse(response: WineryResponse): Wine[] {
    return response.wines.map(r => this.toEntityFromResource(r));
  }

  toEntityFromResource(resource: WineResource): Wine {
    return new Wine({
      id: resource.id,
      winery: resource.winery,
      name: resource.wine,       // SampleAPI uses "wine" for the wine name
      location: resource.location,
      image: resource.image
    });
  }

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
}
```

### `winery/infrastructure/winery-api-endpoint.ts`

```ts
import { HttpClient } from '@angular/common/http';
import { BaseApiEndpoint } from '../../shared/infrastructure/base-api-endpoint';
import { Wine } from '../domain/model/wine.entity';
import { WineResource, WineryResponse } from './winery-response';
import { WineAssembler } from './wine-assembler';
import { environment } from '../../../environments/environment';

/**
 * @summary API endpoint for querying wines by type from SampleAPI.
 * @author Tu Nombre y Apellido
 */
export class WineryApiEndpoint extends BaseApiEndpoint<Wine, WineResource, WineryResponse, WineAssembler> {

  constructor(http: HttpClient, wineType: string) {
    super(
      http,
      `${environment.wineryApiBaseUrl}/${wineType}`,
      new WineAssembler()
    );
  }
}
```

### `winery/infrastructure/winery-api.service.ts`

```ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';
import { BaseApi } from '../../shared/infrastructure/base-api';
import { Wine } from '../domain/model/wine.entity';
import { WineryApiEndpoint } from './winery-api-endpoint';

/**
 * @summary Service that provides access to the SampleAPI Winery endpoints.
 * @author Tu Nombre y Apellido
 */
@Injectable({ providedIn: 'root' })
export class WineryApi extends BaseApi {

  constructor(private http: HttpClient) {
    super();
  }

  /**
   * Retrieves wines by wine type from SampleAPI.
   * @param wineType - The wine type string (e.g., 'reds', 'whites').
   */
  getWinesByType(wineType: string): Observable<Wine[]> {
    const endpoint = new WineryApiEndpoint(this.http, wineType);
    return endpoint.getAll();
  }
}
```

### `winery/application/winery-store.service.ts`

```ts
import { Injectable, signal } from '@angular/core';
import { WineryApi } from '../infrastructure/winery-api.service';
import { Wine } from '../domain/model/wine.entity';

/**
 * @summary State store for winery data (wines by type) using Angular Signals.
 * @author Tu Nombre y Apellido
 */
@Injectable({ providedIn: 'root' })
export class WineryStore {

  private readonly winesSignal = signal<Wine[]>([]);
  private readonly loadingSignal = signal<boolean>(false);
  private readonly errorSignal = signal<string | null>(null);

  readonly wines = this.winesSignal.asReadonly();
  readonly loading = this.loadingSignal.asReadonly();
  readonly error = this.errorSignal.asReadonly();

  readonly wineTypes: string[] = ['reds', 'whites', 'sparkling', 'rose', 'dessert', 'port'];

  constructor(private wineryApi: WineryApi) {}

  /**
   * Loads wines for the given wine type.
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
        this.errorSignal.set(err.message || 'Failed to load wines');
        this.loadingSignal.set(false);
      }
    });
  }

  /** Clears the current wine list. */
  clearWines(): void {
    this.winesSignal.set([]);
  }
}
```

---

## PASO 11 — Dominio Preservation (Cellars & PreservationItems)

### Generar archivos

```bash
ng generate interface preservation/infrastructure/cellar-response
ng generate interface preservation/infrastructure/preservation-item-response
ng generate class preservation/domain/model/cellar --type=entity --skip-tests=true
ng generate class preservation/domain/model/preservation-item --type=entity --skip-tests=true
ng generate class preservation/infrastructure/cellar-assembler --skip-tests=true
ng generate class preservation/infrastructure/preservation-item-assembler --skip-tests=true
ng generate class preservation/infrastructure/cellars-api-endpoint --skip-tests=true
ng generate class preservation/infrastructure/preservation-items-api-endpoint --skip-tests=true
ng generate service preservation/infrastructure/preservation-api --skip-tests=true
ng generate service preservation/application/preservation-store --skip-tests=true
```

### `preservation/infrastructure/cellar-response.ts`

```ts
import { BaseResource, BaseResponse } from '../../shared/infrastructure/base-response';

/**
 * @summary Response structure for cellars from the local API.
 * @author Tu Nombre y Apellido
 */
export interface CellarsResponse extends BaseResponse {
  cellars: CellarResource[];
}

/**
 * @summary Resource/DTO for a Cellar object.
 */
export interface CellarResource extends BaseResource {
  id: number;
  name: string;
  wineType: string;
  capacity: number;
}
```

### `preservation/infrastructure/preservation-item-response.ts`

```ts
import { BaseResource, BaseResponse } from '../../shared/infrastructure/base-response';

/**
 * @summary Response structure for preservation items from the local API.
 * @author Tu Nombre y Apellido
 */
export interface PreservationItemsResponse extends BaseResponse {
  items: PreservationItemResource[];
}

/**
 * @summary Resource/DTO for a PreservationItem object.
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

### `preservation/domain/model/cellar.entity.ts`

```ts
import { BaseEntity } from '../../../shared/infrastructure/base-entity';

/**
 * @summary Domain entity representing a Wine Cellar.
 * @author Tu Nombre y Apellido
 */
export class Cellar implements BaseEntity {
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
}
```

### `preservation/domain/model/preservation-item.entity.ts`

```ts
import { BaseEntity } from '../../../shared/infrastructure/base-entity';

/**
 * @summary Domain entity representing a Preservation Item in a Wine Cellar.
 * @author Tu Nombre y Apellido
 */
export class PreservationItem implements BaseEntity {
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
}
```

### `preservation/infrastructure/cellar-assembler.ts`

```ts
import { BaseAssembler } from '../../shared/infrastructure/base-assembler';
import { Cellar } from '../domain/model/cellar.entity';
import { CellarResource, CellarsResponse } from './cellar-response';

/**
 * @summary Assembler that converts between CellarResource and Cellar entity.
 * @author Tu Nombre y Apellido
 */
export class CellarAssembler implements BaseAssembler<Cellar, CellarResource, CellarsResponse> {

  toEntitiesFromResponse(response: CellarsResponse): Cellar[] {
    return response.cellars.map(r => this.toEntityFromResource(r));
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
}
```

### `preservation/infrastructure/preservation-item-assembler.ts`

```ts
import { BaseAssembler } from '../../shared/infrastructure/base-assembler';
import { PreservationItem } from '../domain/model/preservation-item.entity';
import { PreservationItemResource, PreservationItemsResponse } from './preservation-item-response';

/**
 * @summary Assembler that converts between PreservationItemResource and PreservationItem entity.
 * @author Tu Nombre y Apellido
 */
export class PreservationItemAssembler implements BaseAssembler<PreservationItem, PreservationItemResource, PreservationItemsResponse> {

  toEntitiesFromResponse(response: PreservationItemsResponse): PreservationItem[] {
    return response.items.map(r => this.toEntityFromResource(r));
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
}
```

### `preservation/infrastructure/cellars-api-endpoint.ts`

```ts
import { HttpClient } from '@angular/common/http';
import { BaseApiEndpoint } from '../../shared/infrastructure/base-api-endpoint';
import { Cellar } from '../domain/model/cellar.entity';
import { CellarResource, CellarsResponse } from './cellar-response';
import { CellarAssembler } from './cellar-assembler';
import { environment } from '../../../environments/environment';

/**
 * @summary API endpoint class for Cellars resource.
 * @author Tu Nombre y Apellido
 */
export class CellarsApiEndpoint extends BaseApiEndpoint<Cellar, CellarResource, CellarsResponse, CellarAssembler> {

  constructor(http: HttpClient) {
    super(
      http,
      `${environment.cellarApiBaseUrl}${environment.cellarsEndpointPath}`,
      new CellarAssembler()
    );
  }
}
```

### `preservation/infrastructure/preservation-items-api-endpoint.ts`

```ts
import { HttpClient } from '@angular/common/http';
import { BaseApiEndpoint } from '../../shared/infrastructure/base-api-endpoint';
import { PreservationItem } from '../domain/model/preservation-item.entity';
import { PreservationItemResource, PreservationItemsResponse } from './preservation-item-response';
import { PreservationItemAssembler } from './preservation-item-assembler';
import { environment } from '../../../environments/environment';

/**
 * @summary API endpoint class for PreservationItems resource.
 * @author Tu Nombre y Apellido
 */
export class PreservationItemsApiEndpoint extends BaseApiEndpoint<
  PreservationItem,
  PreservationItemResource,
  PreservationItemsResponse,
  PreservationItemAssembler
> {
  constructor(http: HttpClient) {
    super(
      http,
      `${environment.cellarApiBaseUrl}${environment.preservationItemsEndpointPath}`,
      new PreservationItemAssembler()
    );
  }
}
```

### `preservation/infrastructure/preservation-api.service.ts`

```ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';
import { BaseApi } from '../../shared/infrastructure/base-api';
import { Cellar } from '../domain/model/cellar.entity';
import { PreservationItem } from '../domain/model/preservation-item.entity';
import { CellarsApiEndpoint } from './cellars-api-endpoint';
import { PreservationItemsApiEndpoint } from './preservation-items-api-endpoint';

/**
 * @summary Service that orchestrates Cellar and PreservationItem API endpoints.
 * @author Tu Nombre y Apellido
 */
@Injectable({ providedIn: 'root' })
export class PreservationApi extends BaseApi {

  private readonly cellarsEndpoint: CellarsApiEndpoint;
  private readonly preservationItemsEndpoint: PreservationItemsApiEndpoint;

  constructor(http: HttpClient) {
    super();
    this.cellarsEndpoint = new CellarsApiEndpoint(http);
    this.preservationItemsEndpoint = new PreservationItemsApiEndpoint(http);
  }

  getCellars(): Observable<Cellar[]> { return this.cellarsEndpoint.getAll(); }
  getCellar(id: number): Observable<Cellar> { return this.cellarsEndpoint.getById(id); }

  getPreservationItems(): Observable<PreservationItem[]> { return this.preservationItemsEndpoint.getAll(); }
  createPreservationItem(item: PreservationItem): Observable<PreservationItem> { return this.preservationItemsEndpoint.create(item); }
}
```

### `preservation/application/preservation-store.service.ts`

```ts
import { Injectable, computed, signal } from '@angular/core';
import { takeUntilDestroyed } from '@angular/core/rxjs-interop';
import { retry } from 'rxjs';
import { PreservationApi } from '../infrastructure/preservation-api.service';
import { Cellar } from '../domain/model/cellar.entity';
import { PreservationItem } from '../domain/model/preservation-item.entity';

/**
 * @summary State store for Preservation domain (Cellars and PreservationItems) using Angular Signals.
 * @author Tu Nombre y Apellido
 */
@Injectable({ providedIn: 'root' })
export class PreservationStore {

  private readonly cellarsSignal = signal<Cellar[]>([]);
  private readonly preservationItemsSignal = signal<PreservationItem[]>([]);
  private readonly loadingSignal = signal<boolean>(false);
  private readonly errorSignal = signal<string | null>(null);

  readonly cellars = this.cellarsSignal.asReadonly();
  readonly preservationItems = this.preservationItemsSignal.asReadonly();
  readonly loading = this.loadingSignal.asReadonly();
  readonly error = this.errorSignal.asReadonly();

  /**
   * Returns total bottles count for a given cellar.
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
   * Returns items for a specific cellar.
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

  constructor(private preservationApi: PreservationApi) {
    this.loadCellars();
    this.loadPreservationItems();
  }

  /** Adds a new preservation item. */
  addPreservationItem(item: PreservationItem): void {
    this.loadingSignal.set(true);
    this.errorSignal.set(null);
    this.preservationApi.createPreservationItem(item).pipe(retry(2)).subscribe({
      next: created => {
        this.preservationItemsSignal.update(items => [...items, created]);
        this.loadingSignal.set(false);
      },
      error: err => {
        this.errorSignal.set(err.message || 'Failed to create preservation item');
        this.loadingSignal.set(false);
      }
    });
  }

  private loadCellars(): void {
    this.loadingSignal.set(true);
    this.preservationApi.getCellars().pipe(takeUntilDestroyed()).subscribe({
      next: cellars => {
        this.cellarsSignal.set(cellars);
        this.loadingSignal.set(false);
      },
      error: err => {
        this.errorSignal.set(err.message || 'Failed to load cellars');
        this.loadingSignal.set(false);
      }
    });
  }

  private loadPreservationItems(): void {
    this.loadingSignal.set(true);
    this.preservationApi.getPreservationItems().pipe(takeUntilDestroyed()).subscribe({
      next: items => {
        this.preservationItemsSignal.set(items);
        this.loadingSignal.set(false);
      },
      error: err => {
        this.errorSignal.set(err.message || 'Failed to load preservation items');
        this.loadingSignal.set(false);
      }
    });
  }
}
```

---

## PASO 12 — Generar Componentes

```bash
ng generate component shared/presentation/components/toolbar --skip-tests=true
ng generate component shared/presentation/components/language-switcher --skip-tests=true
ng generate component shared/presentation/components/layout --skip-tests=true
ng generate component shared/presentation/views/home --skip-tests=true
ng generate component shared/presentation/views/page-not-found --skip-tests=true
ng generate component preservation/presentation/components/cellar-summary --skip-tests=true
ng generate component preservation/presentation/views/new-preservation-item --skip-tests=true
```

---

## PASO 13 — Configuración de Rutas

### `preservation/presentation/views/preservation.routes.ts`

**Crear** el archivo manualmente:

```ts
import { Routes } from '@angular/router';

const newPreservationItem = () =>
  import('./new-preservation-item/new-preservation-item').then(m => m.NewPreservationItem);

/**
 * @summary Routes for the Preservation bounded context.
 * @author Tu Nombre y Apellido
 */
export const preservationRoutes: Routes = [
  { path: 'items/new', loadComponent: newPreservationItem, title: 'The Wine Square - New Preservation Item' }
];
```

### `src/app/app.routes.ts`

**Reemplazar** el contenido completo:

```ts
import { Routes } from '@angular/router';
import { Home } from './shared/presentation/views/home/home';

const pageNotFound = () =>
  import('./shared/presentation/views/page-not-found/page-not-found').then(m => m.PageNotFound);

const baseTitle = 'The Wine Square';

/**
 * @summary Application-level routes.
 * @author Tu Nombre y Apellido
 */
export const routes: Routes = [
  { path: 'home', component: Home, title: `${baseTitle} - Home` },
  {
    path: 'preservation',
    loadChildren: () =>
      import('./preservation/presentation/views/preservation.routes').then(m => m.preservationRoutes)
  },
  { path: '', redirectTo: '/home', pathMatch: 'full' },
  { path: '**', loadComponent: pageNotFound, title: `${baseTitle} - Page Not Found` }
];
```

---

## PASO 14 — Componente LanguageSwitcher

### `shared/presentation/components/language-switcher/language-switcher.ts`

```ts
import { Component, inject } from '@angular/core';
import { MatButtonToggleModule } from '@angular/material/button-toggle';
import { TranslateService } from '@ngx-translate/core';

/**
 * @summary Component for switching the application language between EN and ES.
 * @author Tu Nombre y Apellido
 */
@Component({
  selector: 'app-language-switcher',
  standalone: true,
  imports: [MatButtonToggleModule],
  templateUrl: './language-switcher.html',
  styleUrl: './language-switcher.css'
})
export class LanguageSwitcher {
  protected currentLang: string = 'en';
  protected languages: string[] = ['en', 'es'];
  private translate = inject(TranslateService);

  constructor() {
    this.currentLang = this.translate.getCurrentLang() || 'en';
  }

  useLanguage(language: string): void {
    this.translate.use(language);
    this.currentLang = language;
  }
}
```

### `shared/presentation/components/language-switcher/language-switcher.html`

```html
<mat-button-toggle-group
  [value]="currentLang"
  appearance="standard"
  aria-label="Language selector"
  name="language">
  @for (language of languages; track language) {
    <mat-button-toggle
      [value]="language"
      [attr.aria-label]="'Switch to ' + language.toUpperCase()"
      (click)="useLanguage(language)">
      {{ language.toUpperCase() }}
    </mat-button-toggle>
  }
</mat-button-toggle-group>
```

---

## PASO 15 — Componente Layout (Toolbar principal)

### `shared/presentation/components/layout/layout.ts`

```ts
import { Component } from '@angular/core';
import { RouterLink, RouterLinkActive, RouterOutlet } from '@angular/router';
import { MatToolbarModule } from '@angular/material/toolbar';
import { MatButtonModule } from '@angular/material/button';
import { TranslatePipe } from '@ngx-translate/core';
import { LanguageSwitcher } from '../language-switcher/language-switcher';
import { environment } from '../../../../../environments/environment';

/**
 * @summary Main layout component containing the toolbar and router outlet.
 * @author Tu Nombre y Apellido
 */
@Component({
  selector: 'app-layout',
  standalone: true,
  imports: [
    RouterOutlet, RouterLink, RouterLinkActive,
    MatToolbarModule, MatButtonModule,
    TranslatePipe, LanguageSwitcher
  ],
  templateUrl: './layout.html',
  styleUrl: './layout.css'
})
export class Layout {
  protected logoUrl = `${environment.logoApiBaseUrl}/thewinesquare.com?token=pk_DEMO`;

  options = [
    { link: '/home', label: 'nav.home' },
    { link: '/preservation/items/new', label: 'nav.new-preservation-item' }
  ];
}
```

### `shared/presentation/components/layout/layout.html`

```html
<mat-toolbar color="primary" role="banner" aria-label="Main navigation toolbar">
  <img [src]="logoUrl" alt="The Wine Square logo" height="36" style="margin-right: 10px;" />
  <span>{{ 'toolbar.title' | translate }}</span>
  <span class="spacer"></span>
  @for (option of options; track option.label) {
    <a mat-button
       [routerLink]="option.link"
       routerLinkActive="active-link"
       [attr.aria-label]="option.label | translate">
      {{ option.label | translate }}
    </a>
  }
  <app-language-switcher aria-label="Language switcher" />
</mat-toolbar>

<main role="main">
  <router-outlet />
</main>
```

### `shared/presentation/components/layout/layout.css`

```css
.spacer {
  flex: 1 1 auto;
}

.active-link {
  font-weight: bold;
  border-bottom: 2px solid white;
}

main {
  padding: 24px;
  min-height: calc(100vh - 64px);
}
```

---

## PASO 16 — Componente CellarSummary

### `preservation/presentation/components/cellar-summary/cellar-summary.ts`

```ts
import { Component, Input, inject, computed } from '@angular/core';
import { MatCardModule } from '@angular/material/card';
import { TranslatePipe } from '@ngx-translate/core';
import { Cellar } from '../../../domain/model/cellar.entity';
import { PreservationStore } from '../../../application/preservation-store.service';

/**
 * @summary Component that displays a summary card for a Wine Cellar.
 * @author Tu Nombre y Apellido
 */
@Component({
  selector: 'app-cellar-summary',
  standalone: true,
  imports: [MatCardModule, TranslatePipe],
  templateUrl: './cellar-summary.html',
  styleUrl: './cellar-summary.css'
})
export class CellarSummary {
  @Input() cellar!: Cellar;

  private store = inject(PreservationStore);

  get items() {
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
}
```

### `preservation/presentation/components/cellar-summary/cellar-summary.html`

```html
<mat-card role="article" [attr.aria-label]="cellar.name + ' cellar summary'">
  <mat-card-header>
    <mat-card-title>{{ cellar.name }}</mat-card-title>
    <mat-card-subtitle>{{ cellar.wineType | titlecase }}</mat-card-subtitle>
  </mat-card-header>

  <mat-card-content>
    @if (isEmpty) {
      <p aria-live="polite">{{ 'home.empty' | translate }}</p>
    } @else {
      <ul aria-label="Wines in cellar">
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

### `preservation/presentation/components/cellar-summary/cellar-summary.css`

```css
mat-card {
  margin: 8px;
}

mat-card-footer {
  padding: 8px 16px;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  padding: 4px 0;
  border-bottom: 1px solid #eee;
}
```

---

## PASO 17 — Vista Home

### `shared/presentation/views/home/home.ts`

```ts
import { Component, inject } from '@angular/core';
import { MatGridListModule } from '@angular/material/grid-list';
import { TranslatePipe } from '@ngx-translate/core';
import { PreservationStore } from '../../../../preservation/application/preservation-store.service';
import { CellarSummary } from '../../../../preservation/presentation/components/cellar-summary/cellar-summary';

/**
 * @summary Home view displaying the list of Wine Cellars.
 * @author Tu Nombre y Apellido
 */
@Component({
  selector: 'app-home',
  standalone: true,
  imports: [MatGridListModule, TranslatePipe, CellarSummary],
  templateUrl: './home.html',
  styleUrl: './home.css'
})
export class Home {
  protected store = inject(PreservationStore);
}
```

### `shared/presentation/views/home/home.html`

```html
<section aria-labelledby="home-title">
  <h1 id="home-title">{{ 'home.title' | translate }}</h1>
  <p>{{ 'home.content' | translate }}</p>

  <h2>{{ 'home.my-wine-cellars' | translate }}</h2>

  @if (store.loading()) {
    <p aria-live="polite">Loading cellars...</p>
  }

  @if (store.error()) {
    <p role="alert" style="color: red;">{{ store.error() }}</p>
  }

  <mat-grid-list cols="2" rowHeight="fit" gutterSize="16px" aria-label="Wine cellars grid">
    @for (cellar of store.cellars(); track cellar.id) {
      <mat-grid-tile>
        <app-cellar-summary [cellar]="cellar" />
      </mat-grid-tile>
    }
  </mat-grid-list>
</section>
```

### `shared/presentation/views/home/home.css`

```css
section {
  max-width: 1200px;
  margin: 0 auto;
}

h1 {
  margin-bottom: 4px;
}

h2 {
  margin-top: 32px;
  margin-bottom: 16px;
}

mat-grid-list {
  width: 100%;
}
```

---

## PASO 18 — Vista New Preservation Item

### `preservation/presentation/views/new-preservation-item/new-preservation-item.ts`

```ts
import { Component, inject } from '@angular/core';
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

/**
 * @summary View for creating a new Preservation Item (adding wine bottles to a cellar).
 * @author Tu Nombre y Apellido
 */
@Component({
  selector: 'app-new-preservation-item',
  standalone: true,
  imports: [
    ReactiveFormsModule,
    MatFormFieldModule, MatSelectModule, MatInputModule, MatButtonModule,
    TranslatePipe
  ],
  templateUrl: './new-preservation-item.html',
  styleUrl: './new-preservation-item.css'
})
export class NewPreservationItem {
  private fb = inject(FormBuilder);
  private router = inject(Router);
  protected preservationStore = inject(PreservationStore);
  protected wineryStore = inject(WineryStore);

  form = this.fb.group({
    wineType: new FormControl<string>('', { nonNullable: true, validators: [Validators.required] }),
    wineId: new FormControl<number | null>(null, [Validators.required]),
    wineName: new FormControl<string>('', { nonNullable: true }),
    quantity: new FormControl<number | null>(null, [Validators.required, Validators.min(1)])
  });

  get availableCapacity(): number {
    const wineType = this.form.value.wineType;
    if (!wineType) return 0;
    const cellar = this.preservationStore.getCellarByWineType(wineType);
    return cellar ? this.preservationStore.getAvailableCapacity(cellar.id) : 0;
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
    const cellar = this.preservationStore.getCellarByWineType(wineType);
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

    this.preservationStore.addPreservationItem(item);
    this.router.navigate(['/home']);
  }

  cancel(): void {
    this.router.navigate(['/home']);
  }
}
```

### `preservation/presentation/views/new-preservation-item/new-preservation-item.html`

```html
<section aria-labelledby="form-title">
  <h1 id="form-title">{{ 'preservation.title' | translate }}</h1>
  <h2>{{ 'preservation.subtitle' | translate }}</h2>

  <form [formGroup]="form" (ngSubmit)="submit()" aria-label="New preservation item form">

    <!-- Wine Type -->
    <mat-form-field appearance="outline">
      <mat-label>{{ 'preservation.wine-type' | translate }}</mat-label>
      <mat-select formControlName="wineType"
                  (selectionChange)="onWineTypeChange($event.value)"
                  aria-required="true">
        @for (type of wineryStore.wineTypes; track type) {
          <mat-option [value]="type">{{ type | titlecase }}</mat-option>
        }
      </mat-select>
      @if (form.get('wineType')?.touched && form.get('wineType')?.hasError('required')) {
        <mat-error>{{ 'preservation.wine-type-required' | translate }}</mat-error>
      }
    </mat-form-field>

    <!-- Wine -->
    <mat-form-field appearance="outline">
      <mat-label>{{ 'preservation.wine' | translate }}</mat-label>
      <mat-select formControlName="wineId"
                  (selectionChange)="onWineChange($event.value)"
                  [disabled]="!form.value.wineType"
                  aria-required="true">
        @if (wineryStore.loading()) {
          <mat-option disabled>Loading wines...</mat-option>
        }
        @for (wine of wineryStore.wines(); track wine.id) {
          <mat-option [value]="wine.id">{{ wine.name }}</mat-option>
        }
      </mat-select>
      @if (form.get('wineId')?.touched && form.get('wineId')?.hasError('required')) {
        <mat-error>{{ 'preservation.wine-required' | translate }}</mat-error>
      }
    </mat-form-field>

    <!-- Quantity -->
    <mat-form-field appearance="outline">
      <mat-label>{{ 'preservation.quantity' | translate }}</mat-label>
      <input matInput
             type="number"
             formControlName="quantity"
             [max]="availableCapacity"
             min="1"
             aria-required="true"
             [attr.aria-describedby]="'capacity-hint'" />
      <mat-hint id="capacity-hint">Available capacity: {{ availableCapacity }}</mat-hint>
      @if (form.get('quantity')?.touched && form.get('quantity')?.hasError('required')) {
        <mat-error>{{ 'preservation.quantity-required' | translate }}</mat-error>
      }
      @if (form.get('quantity')?.value && !isQuantityValid()) {
        <mat-error>{{ 'preservation.quantity-exceeded' | translate }}</mat-error>
      }
    </mat-form-field>

    <!-- Actions -->
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
              aria-label="Cancel and go home">
        {{ 'preservation.cancel' | translate }}
      </button>
    </div>
  </form>
</section>
```

### `preservation/presentation/views/new-preservation-item/new-preservation-item.css`

```css
section {
  max-width: 600px;
  margin: 0 auto;
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

## PASO 19 — Vista Page Not Found

### `shared/presentation/views/page-not-found/page-not-found.ts`

```ts
import { Component, inject } from '@angular/core';
import { Router, RouterLink } from '@angular/router';
import { MatButtonModule } from '@angular/material/button';
import { TranslatePipe } from '@ngx-translate/core';

/**
 * @summary View displayed when a navigation route is not found (404).
 * @author Tu Nombre y Apellido
 */
@Component({
  selector: 'app-page-not-found',
  standalone: true,
  imports: [MatButtonModule, RouterLink, TranslatePipe],
  templateUrl: './page-not-found.html',
  styleUrl: './page-not-found.css'
})
export class PageNotFound {
  private router = inject(Router);
  protected invalidPath: string = this.router.url;
}
```

### `shared/presentation/views/page-not-found/page-not-found.html`

```html
<section aria-labelledby="not-found-title">
  <h1 id="not-found-title">{{ 'page-not-found.title' | translate }}</h1>
  <p [innerHTML]="('page-not-found.content' | translate : { path: invalidPath })"></p>
  <a mat-raised-button color="primary" routerLink="/home" aria-label="Go back to home">
    {{ 'page-not-found.go-home' | translate }}
  </a>
</section>
```

### `shared/presentation/views/page-not-found/page-not-found.css`

```css
section {
  text-align: center;
  margin-top: 80px;
}

h1 {
  font-size: 2rem;
  margin-bottom: 16px;
}

p {
  margin-bottom: 24px;
}
```

---

## PASO 20 — Componente App raíz

### `src/app/app.ts`

```ts
import { Component } from '@angular/core';
import { Layout } from './shared/presentation/components/layout/layout';

/**
 * @summary Root application component.
 * @author Tu Nombre y Apellido
 */
@Component({
  selector: 'app-root',
  standalone: true,
  imports: [Layout],
  template: '<app-layout />'
})
export class App {}
```

---

## PASO 21 — Estilos globales

### `src/styles.css`

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Roboto, 'Helvetica Neue', sans-serif;
}

h1, h2, h3 {
  color: #4a1942;
}

mat-grid-tile {
  overflow: visible !important;
}
```

---

## PASO 22 — README.md

**Crear/reemplazar** el archivo `README.md` en la raíz del proyecto:

```markdown
# The Wine Square — Cellar Management Platform

## Description
A frontend web application built for **The Wine Square**, allowing clients to manage their Wine Cellars and register Preservation Items.

## Features
- View all Wine Cellars with their current wine inventory
- Add new Preservation Items (wine bottles) to a cellar
- Dynamic wine selection based on wine type via SampleAPI
- Automatic cellar assignment based on wine type
- Capacity validation before adding items
- Multilingual support: English (default) and Spanish
- Page not found view for invalid routes

## Tech Stack
- **Angular** v21+ (Standalone Components, Signals, Router)
- **Angular Material** (UI components)
- **@ngx-translate/core** (i18n)
- **JSON Server** v0.17.4 (mock backend)
- **TypeScript** (strict mode)
- **HttpClient** (@angular/common/http)

## Configuration

### Prerequisites
- Node.js 20+
- Angular CLI 21+
- JSON Server 0.17.4 (`npm install -g json-server@0.17.4`)

### Running the mock backend
```bash
cd server
json-server --watch db.json
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

## PASO 23 — Verificación final antes de entregar

1. Asegúrate que el `json-server` esté corriendo y los endpoints respondan:
   - `http://localhost:3000/cellars`
   - `http://localhost:3000/preservation-items`

2. Ejecuta la app sin errores:
   ```bash
   ng serve --port 4200
   ```

3. Verifica las rutas:
   - `/` → redirige a `/home`
   - `/home` → vista Home con grid de cellars
   - `/preservation/items/new` → formulario New Preservation Item
   - Cualquier ruta inválida → vista Page Not Found

4. **Elimina** la carpeta `node_modules` antes de empaquetar:
   ```bash
   rm -rf node_modules
   ```

5. Genera el ZIP con el nombre correcto:
   ```bash
   zip -r ea20262u<TU-CODIGO>.zip . -x "*.git*"
   ```

---

> **Tip final:** Reemplaza todas las ocurrencias de `Tu Nombre y Apellido` y `<TU-CODIGO>` con tus datos reales antes de entregar.
