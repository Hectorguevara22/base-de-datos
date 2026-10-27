```mermaid
classDiagram

%%====================capa modelo==================================%%
        class Departamento {
    Number idDepartamento;
    String nombre;
    String codigoDane;
}


class Municipio {
    Number idMunicipio;
    Number idDepartamento;
    String nombre;
    String codigoDane;
}

class Comuna {
    Number idComuna;
    Number idMunicipio;
    String nombre;
}

class Barrio {
    Number idBarrio;
    Number idMunicipio;
    Number idComuna;
    String nombre;
}

class Direccion {
    Number idDireccion;
    Number idBarrio;
    String calle;
    String numero;
    String complemento;
    String codigoPostal;
    String referencia;
}

class DireccionUsuario {
    Number idUsuario;
    Number idDireccion;
    String alias;
    char esPrincipal;
}

class Usuario {
    Number idUsuario;
    String tipoDocumento;
    String numDocumento;
    String primerNombre;
    String segundoNombre;
    String primerApellido;
    String segundoApellido;
    String correo;
    String telefono;
    String contrasenaHash;
    String rol;
    String estado;
    Timestamp fechaRegistro;
}

class Empleado  {
    Number idSucursal;
    String cargo;
    Number salario;
    Date fechaContratacion;
    String estado;
}

class Empresa {
    Number idEmpresa;
    String nombre;
    String nit;
    String correo;
    String telefono;
}

class Sucursal {
    Number idSucursal;
    Number idEmpresa;
    Number idDireccion;
    String nombre;
    String telefono;
    String estado;
}

class Socio {
    Number idSocio;
    String tipo;
    String nombreCompania;
    String nit;
    String correo;
    String telefono;
    Number idDireccion;
    String estado;
}

class Proveedor {
    String tipo;
    Interval tiempoEntrega;
}

class Taller  {
    String tipo;
    String descrEspecialidad;
    Number espaciosDisponibles;
}

class Tarifa {
    Number idTarifa;
    String nombre;
    Number porcentaje;
}

class Afiliacion {
    Number idAfiliacion;
    Number idSocio;
    Number idTarifa;
    Date fechaAfiliacion;
    Date fechaVence;
    String estado;
}

class Marca {
    Number idMarca;
    String nombre;
}

class Categoria {
    Number idCategoria;
    Number idCategoriaPadre;
    String nombre;
}

class Componente {
    Number idComponente;
    String tipo;
    String nombre;
    String descripcion;
    String referencia;
    Number idMarca;
    Number idCategoria;
    Number precio;
    String estado;
}

class Llanta {
    Number anchoMm;
    char indiceVelocidad;
}

class Rin  {
    Number diametro;
    String material;
}

class Motor {
    Number cilindraje;
    Number potencia;
}

class Transmision {
    String tipoTransmision;
    Number nVelocidades;
}

class Vehiculo {
    Number idVehiculo;
    String tipo;
    Number idMarca;
    String nombreModelo;
    Number anioFabricacion;
}

class Motocicleta  {
    String tipoMoto;
}

class Coche {
    String tipoCarroceria;
}

class Compatibilidad {
    Number idCompatibilidad;
    Number idComponente;
    Number idVehiculo;
    Number anioDesde;
    Number anioHasta;
}

class Almacen {
    Number idAlmacen;
    Number idEmpresa;
    Number idProveedor;
    Number idDireccion;
    String nombre;
    String estado;
}

class Inventario {
    Number idInventario;
    Number idAlmacen;
    Number idComponente;
    Number stock;
    Number stockMinimo;
    Timestamp fechaActualizacion;
}

class Compra {
    Number idCompra;
    Number idProveedor;
    Number idAlmacenDestino;
    Number idUsuario;
    Timestamp fecha;
    Number total;
    String estado;
}

class DetalleCompra {
    Number idDetalleCompra;
    Number idCompra;
    Number idComponente;
    Number cantidad;
    Number costoUnitario;
    Number subtotal;
}

class Servicio {
    Number idServicio;
    Number idTaller;
    String nombre;
    String descripcion;
    Number precioBase;
    Interval duracion;
    char estaDisponible;
}

class MetodoPago {
    Number idMetodoPago;
    String nombre;
    String descripcion;
    char estaActivo;
}

class Transaccion {
    Number idTransaccion;
    Number idUsuario;
    Number idEmpleado;
    Number idSucursal;
    Timestamp fecha;
    Number total;
    String estado;
}

class DetalleTransaccion {
    Number idDetalle;
    Number idTransaccion;
    Number idComponente;
    Number idAlmacen;
    Number cantidad;
    Number precioUnitario;
    Number descuento;
    Number impuestoPct;
    Number subtotal;
}

class DetalleServicio {
    Number idDetalleServicio;
    Number idTransaccion;
    Number idServicio;
    Number cantidad;
    Number precioUnitario;
    Number descuento;
    Number impuestoPct;
    Timestamp fechaProgramada;
    String estado;
    Number subtotal;
}

class Pago {
    Number idPago;
    Number idTransaccion;
    Number idMetodoPago;
    Number monto;
    Timestamp fechaPago;
    String estado;
    String referencia;
}

class Envio {
    Number idEnvio;
    Number idTransaccion;
    Number idDireccion;
    String transportadora;
    String numeroGuia;
    Date fechaEnvio;
    Date fechaRecepcion;
    String estado;
}

class MovimientoInventario {
    Number idMovimiento;
    String tipo;
    String motivo;
    Number idAlmacenOrigen;
    Number idAlmacenDestino;
    Number idUsuario;
    Number idTransaccion;
    Number idCompra;
    Timestamp fecha;
    String estado;
    String observacion;
}

class DetalleMovimiento {
    Number idDetalleMovimiento;
    Number idMovimiento;
    Number idComponente;
    Number cantidad;
}
Usuario <-- Empleado

Socio <-- Proveedor
Socio <-- Taller

Componente <-- Llanta
Componente <-- Rin
Componente <-- Motor
Componente <-- Transmision

Vehiculo <-- Motocicleta
Vehiculo <-- Coche

%%====================capa persistencia==================================%%

class DepartamentoRepository {
    - departamentos: List<Departamento>
    + guardar(departamento: Departamento): Departamento
    + buscarPorId(id: int): Departamento
    + listarTodos(): List<Departamento>
    + actualizar(departamento: Departamento): boolean
    + eliminar(id: int): boolean
}
class MunicipioRepository {
    - municipios: List<Municipio>
    + guardar(municipio: Municipio): Municipio
    + buscarPorId(id: int): Municipio
    + listarTodos(): List<Municipio>
    + buscarPorDepartamento(idDepartamento: int): List<Municipio>
    + actualizar(municipio: Municipio): boolean
    + eliminar(id: int): boolean
}
class ComunaRepository {
    - comunas: List<Comuna>
    + guardar(comuna: Comuna): Comuna
    + buscarPorId(id: int): Comuna
    + listarTodos(): List<Comuna>
    + buscarPorMunicipio(idMunicipio: int): List<Comuna>
    + actualizar(comuna: Comuna): boolean
    + eliminar(id: int): boolean
}
class BarrioRepository {
    - barrios: List<Barrio>
    + guardar(barrio: Barrio): Barrio
    + buscarPorId(id: int): Barrio
    + listarTodos(): List<Barrio>
    + buscarPorMunicipio(idMunicipio: int): List<Barrio>
    + buscarPorComuna(idComuna: int): List<Barrio>
    + actualizar(barrio: Barrio): boolean
    + eliminar(id: int): boolean
}
class DireccionRepository {
    - direcciones: List<Direccion>
    + guardar(direccion: Direccion): Direccion
    + buscarPorId(id: int): Direccion
    + listarTodos(): List<Direccion>
    + buscarPorBarrio(idBarrio: int): List<Direccion>
    + actualizar(direccion: Direccion): boolean
    + eliminar(id: int): boolean
}

class DireccionUsuarioRepository {
    - direccionesUsuario: List<DireccionUsuario>
    + guardar(direccionUsuario: DireccionUsuario): DireccionUsuario
    + buscarPorIdUsuario(idUsuario: int): List<DireccionUsuario>
    + listarTodos(): List<DireccionUsuario>
    + actualizar(direccionUsuario: DireccionUsuario): boolean
    + eliminar(idUsuario: int, idDireccion: int): boolean
}

class UsuarioRepository {
    - usuarios: List<Usuario>
    + guardar(usuario: Usuario): Usuario
    + buscarPorId(id: int): Usuario
    + buscarPorDocumento(documento: String): Usuario
    + buscarPorCorreo(correo: String): Usuario
    + listarTodos(): List<Usuario>
    + actualizar(usuario: Usuario): boolean
    + eliminar(id: int): boolean
}





class SucursalRepository {
    - sucursales: List<Sucursal>
    + guardar(sucursal: Sucursal): Sucursal
    + buscarPorId(id: int): Sucursal
    + listarTodos(): List<Sucursal>
    + buscarPorEmpresa(idEmpresa: int): List<Sucursal>
    + actualizar(sucursal: Sucursal): boolean
    + eliminar(id: int): boolean
}

class SocioRepository {
    - socios: List<Socio>
    + guardar(socio: Socio): Socio
    + buscarPorId(id: int): Socio
    + buscarPorNit(nit: String): Socio
    + listarTodos(): List<Socio>
    + actualizar(socio: Socio): boolean
    + eliminar(id: int): boolean
}


class TarifaRepository {
    - tarifas: List<Tarifa>
    + guardar(tarifa: Tarifa): Tarifa
    + buscarPorId(id: int): Tarifa
    + listarTodos(): List<Tarifa>
    + actualizar(tarifa: Tarifa): boolean
    + eliminar(id: int): boolean
}

class AfiliacionRepository {
    - afiliaciones: List<Afiliacion>
    + guardar(afiliacion: Afiliacion): Afiliacion
    + buscarPorId(id: int): Afiliacion
    + listarTodos(): List<Afiliacion>
    + buscarPorSocio(idSocio: int): List<Afiliacion>
    + actualizar(afiliacion: Afiliacion): boolean
    + eliminar(id: int): boolean
}

class MarcaRepository {
    - marcas: List<Marca>
    + guardar(marca: Marca): Marca
    + buscarPorId(id: int): Marca
    + listarTodos(): List<Marca>
    + actualizar(marca: Marca): boolean
    + eliminar(id: int): boolean
}

class CategoriaRepository {
    - categorias: List<Categoria>
    + guardar(categoria: Categoria): Categoria
    + buscarPorId(id: int): Categoria
    + listarTodos(): List<Categoria>
    + buscarPorCategoriaPadre(idPadre: int): List<Categoria>
    + actualizar(categoria: Categoria): boolean
    + eliminar(id: int): boolean
}

class ComponenteRepository {
    - componentes: List<Componente>
    + guardar(componente: Componente): Componente
    + buscarPorId(id: int): Componente
    + listarTodos(): List<Componente>
    + buscarPorMarca(idMarca: int): List<Componente>
    + buscarPorCategoria(idCategoria: int): List<Componente>
    + actualizar(componente: Componente): boolean
    + eliminar(id: int): boolean
}



class VehiculoRepository {
    - vehiculos: List<Vehiculo>
    + guardar(vehiculo: Vehiculo): Vehiculo
    + buscarPorId(id: int): Vehiculo
    + listarTodos(): List<Vehiculo>
    + buscarPorMarca(idMarca: int): List<Vehiculo>
    + actualizar(vehiculo: Vehiculo): boolean
    + eliminar(id: int): boolean
}



class CompatibilidadRepository {
    - compatibilidades: List<Compatibilidad>
    + guardar(compatibilidad: Compatibilidad): Compatibilidad
    + buscarPorId(id: int): Compatibilidad
    + listarTodos(): List<Compatibilidad>
    + buscarPorVehiculo(idVehiculo: int): List<Compatibilidad>
    + buscarPorComponente(idComponente: int): List<Compatibilidad>
    + eliminar(id: int): boolean
}

 class AlmacenRepository {
    - almacenes: List<Almacen>
    + guardar(almacen: Almacen): Almacen
    + buscarPorId(id: int): Almacen
    + listarTodos(): List<Almacen>
    + buscarPorEmpresa(idEmpresa: int): List<Almacen>
    + buscarPorProveedor(idProveedor: int): List<Almacen>
    + actualizar(almacen: Almacen): boolean
    + eliminar(id: int): boolean
}

class InventarioRepository {
    - inventarios: List<Inventario>
    + guardar(inventario: Inventario): Inventario
    + buscarPorId(id: int): Inventario
    + listarTodos(): List<Inventario>
    + buscarPorAlmacen(idAlmacen: int): List<Inventario>
    + buscarPorComponente(idComponente: int): List<Inventario>
    + actualizar(inventario: Inventario): boolean
    + eliminar(id: int): boolean
}

class CompraRepository {
    - compras: List<Compra>
    + guardar(compra: Compra): Compra
    + buscarPorId(id: int): Compra
    + listarTodos(): List<Compra>
    + buscarPorProveedor(idProveedor: int): List<Compra>
    + actualizar(compra: Compra): boolean
    + eliminar(id: int): boolean
}

class DetalleCompraRepository {
    - detalles: List<DetalleCompra>
    + guardar(detalle: DetalleCompra): DetalleCompra
    + buscarPorId(id: int): DetalleCompra
    + listarTodos(): List<DetalleCompra>
    + buscarPorCompra(idCompra: int): List<DetalleCompra>
    + actualizar(detalle: DetalleCompra): boolean
    + eliminar(id: int): boolean
}

class ServicioRepository {
    - servicios: List<Servicio>
    + guardar(servicio: Servicio): Servicio
    + buscarPorId(id: int): Servicio
    + listarTodos(): List<Servicio>
    + buscarPorTaller(idTaller: int): List<Servicio>
    + actualizar(servicio: Servicio): boolean
    + eliminar(id: int): boolean
}

class MetodoPagoRepository {
    - metodosPago: List<MetodoPago>
    + guardar(metodo: MetodoPago): MetodoPago
    + buscarPorId(id: int): MetodoPago
    + listarTodos(): List<MetodoPago>
    + actualizar(metodo: MetodoPago): boolean
    + eliminar(id: int): boolean
}

class TransaccionRepository {
    - transacciones: List<Transaccion>
    + guardar(transaccion: Transaccion): Transaccion
    + buscarPorId(id: int): Transaccion
    + listarTodos(): List<Transaccion>
    + buscarPorUsuario(idUsuario: int): List<Transaccion>
    + buscarPorSucursal(idSucursal: int): List<Transaccion>
    + actualizar(transaccion: Transaccion): boolean
    + eliminar(id: int): boolean
}

class DetalleTransaccionRepository {
    - detalles: List<DetalleTransaccion>
    + guardar(detalle: DetalleTransaccion): DetalleTransaccion
    + buscarPorId(id: int): DetalleTransaccion
    + listarTodos(): List<DetalleTransaccion>
    + buscarPorTransaccion(idTransaccion: int): List<DetalleTransaccion>
    + actualizar(detalle: DetalleTransaccion): boolean
    + eliminar(id: int): boolean
}

class DetalleServicioRepository {
    - detalles: List<DetalleServicio>
    + guardar(detalle: DetalleServicio): DetalleServicio
    + buscarPorId(id: int): DetalleServicio
    + listarTodos(): List<DetalleServicio>
    + buscarPorTransaccion(idTransaccion: int): List<DetalleServicio>
    + actualizar(detalle: DetalleServicio): boolean
    + eliminar(id: int): boolean
}

class PagoRepository {
    - pagos: List<Pago>
    + guardar(pago: Pago): Pago
    + buscarPorId(id: int): Pago
    + listarTodos(): List<Pago>
    + buscarPorTransaccion(idTransaccion: int): List<Pago>
    + actualizar(pago: Pago): boolean
    + eliminar(id: int): boolean
}

class EnvioRepository {
    - envios: List<Envio>
    + guardar(envio: Envio): Envio
    + buscarPorId(id: int): Envio
    + buscarPorTransaccion(idTransaccion: int): Envio
    + listarTodos(): List<Envio>
    + actualizar(envio: Envio): boolean
    + eliminar(id: int): boolean
}

class MovimientoInventarioRepository {
    - movimientos: List<MovimientoInventario>
    + guardar(movimiento: MovimientoInventario): MovimientoInventario
    + buscarPorId(id: int): MovimientoInventario
    + listarTodos(): List<MovimientoInventario>
    + buscarPorAlmacen(idAlmacen: int): List<MovimientoInventario>
    + actualizar(movimiento: MovimientoInventario): boolean
    + eliminar(id: int): boolean
}

class DetalleMovimientoRepository {
    - detalles: List<DetalleMovimiento>
    + guardar(detalle: DetalleMovimiento): DetalleMovimiento
    + buscarPorId(id: int): DetalleMovimiento
    + listarTodos(): List<DetalleMovimiento>
    + buscarPorMovimiento(idMovimiento: int): List<DetalleMovimiento>
    + actualizar(detalle: DetalleMovimiento): boolean
    + eliminar(id: int): boolean
}

DepartamentoRepository <-- Departamento
MunicipioRepository <-- Municipio
ComunaRepository <-- Comuna
BarrioRepository <-- Barrio
DireccionRepository <-- Direccion
DireccionUsuarioRepository <-- DireccionUsuario

UsuarioRepository <-- Usuario
EmpresaRepository <-- Empresa
SucursalRepository <-- Sucursal
SocioRepository <-- Socio
TarifaRepository <-- Tarifa
AfiliacionRepository <-- Afiliacion

MarcaRepository <-- Marca
CategoriaRepository <-- Categoria
ComponenteRepository <-- Componente


VehiculoRepository <-- Vehiculo
CompatibilidadRepository <-- Compatibilidad

AlmacenRepository <-- Almacen
InventarioRepository <-- Inventario
CompraRepository <-- Compra
DetalleCompraRepository <-- DetalleCompra

ServicioRepository <-- Servicio
MetodoPagoRepository <-- MetodoPago
TransaccionRepository <-- Transaccion
DetalleTransaccionRepository <-- DetalleTransaccion
DetalleServicioRepository <-- DetalleServicio
PagoRepository <-- Pago
EnvioRepository <-- Envio

MovimientoInventarioRepository <-- MovimientoInventario
DetalleMovimientoRepository <-- DetalleMovimiento

%%====================capa servicios==================================%%

class DepartamentoService {
    - departamentoRepository: DepartamentoRepository
    + crear(departamento: Departamento): Departamento
    + buscarPorId(id: int): Departamento
    + listarTodos(): List<Departamento>
    + actualizar(departamento: Departamento): boolean
    + eliminar(id: int): boolean
}
class MunicipioService {
    - municipioRepository: MunicipioRepository
    - departamentoRepository: DepartamentoRepository
    + crear(municipio: Municipio): Municipio
    + buscarPorId(id: int): Municipio
    + listarTodos(): List<Municipio>
    + buscarPorDepartamento(idDepartamento: int): List<Municipio>
    + actualizar(municipio: Municipio): boolean
    + eliminar(id: int): boolean
}
class ComunaService {
    - comunaRepository: ComunaRepository
    - municipioRepository: MunicipioRepository
    + crear(comuna: Comuna): Comuna
    + buscarPorId(id: int): Comuna
    + listarTodos(): List<Comuna>
    + buscarPorMunicipio(idMunicipio: int): List<Comuna>
    + actualizar(comuna: Comuna): boolean
    + eliminar(id: int): boolean
}
class BarrioService {
    - barrioRepository: BarrioRepository
    - municipioRepository: MunicipioRepository
    - comunaRepository: ComunaRepository
    + crear(barrio: Barrio): Barrio
    + buscarPorId(id: int): Barrio
    + listarTodos(): List<Barrio>
    + buscarPorMunicipio(idMunicipio: int): List<Barrio>
    + buscarPorComuna(idComuna: int): List<Barrio>
    + actualizar(barrio: Barrio): boolean
    + eliminar(id: int): boolean
}
class DireccionService {
    - direccionRepository: DireccionRepository
    - barrioRepository: BarrioRepository
    + crear(direccion: Direccion): Direccion
    + buscarPorId(id: int): Direccion
    + listarTodos(): List<Direccion>
    + buscarPorBarrio(idBarrio: int): List<Direccion>
    + actualizar(direccion: Direccion): boolean
    + eliminar(id: int): boolean
}
class DireccionUsuarioService {
    - direccionUsuarioRepository: DireccionUsuarioRepository
    - usuarioRepository: UsuarioRepository
    - direccionRepository: DireccionRepository
    + asignar(direccionUsuario: DireccionUsuario): DireccionUsuario
    + buscarPorUsuario(idUsuario: int): List<DireccionUsuario>
    + establecerPrincipal(idUsuario: int, idDireccion: int): boolean
    + eliminar(idUsuario: int, idDireccion: int): boolean
}

class UsuarioService {
    - usuarioRepository: UsuarioRepository
    + registrar(usuario: Usuario): Usuario
    + buscarPorId(id: int): Usuario
    + buscarPorDocumento(documento: String): Usuario
    + buscarPorCorreo(correo: String): Usuario
    + listarTodos(): List<Usuario>
    + actualizar(usuario: Usuario): boolean
    + cambiarEstado(id: int, estado: String): boolean
    + eliminar(id: int): boolean
}



class EmpresaService {
    - empresaRepository: EmpresaRepository
    + crear(empresa: Empresa): Empresa
    + buscarPorId(id: int): Empresa
    + buscarPorNit(nit: String): Empresa
    + listarTodos(): List<Empresa>
    + actualizar(empresa: Empresa): boolean
    + eliminar(id: int): boolean
}

class SucursalService {
    - sucursalRepository: SucursalRepository
    - empresaRepository: EmpresaRepository
    - direccionRepository: DireccionRepository
    + crear(sucursal: Sucursal): Sucursal
    + buscarPorId(id: int): Sucursal
    + listarTodos(): List<Sucursal>
    + buscarPorEmpresa(idEmpresa: int): List<Sucursal>
    + actualizar(sucursal: Sucursal): boolean
    + cambiarEstado(id: int, estado: String): boolean
    + eliminar(id: int): boolean
}
class SocioService {
    - socioRepository: SocioRepository
    + crear(socio: Socio): Socio
    + buscarPorId(id: int): Socio
    + buscarPorNit(nit: String): Socio
    + listarTodos(): List<Socio>
    + actualizar(socio: Socio): boolean
    + cambiarEstado(id: int, estado: String): boolean
    + eliminar(id: int): boolean
}

class TarifaService {
    - tarifaRepository: TarifaRepository
    + crear(tarifa: Tarifa): Tarifa
    + buscarPorId(id: int): Tarifa
    + listarTodos(): List<Tarifa>
    + actualizar(tarifa: Tarifa): boolean
    + eliminar(id: int): boolean
}
class AfiliacionService {
    - afiliacionRepository: AfiliacionRepository
    - socioRepository: SocioRepository
    - tarifaRepository: TarifaRepository
    + crear(afiliacion: Afiliacion): Afiliacion
    + buscarPorId(id: int): Afiliacion
    + listarTodos(): List<Afiliacion>
    + buscarPorSocio(idSocio: int): List<Afiliacion>
    + renovar(id: int, fechaVence: LocalDate): boolean
    + cambiarEstado(id: int, estado: String): boolean
    + eliminar(id: int): boolean
}


class MarcaService {
    - marcaRepository: MarcaRepository
    + crear(marca: Marca): Marca
    + buscarPorId(id: int): Marca
    + listarTodos(): List<Marca>
    + actualizar(marca: Marca): boolean
    + eliminar(id: int): boolean
}
class CategoriaService {
    - categoriaRepository: CategoriaRepository
    + crear(categoria: Categoria): Categoria
    + buscarPorId(id: int): Categoria
    + listarTodos(): List<Categoria>
    + buscarPorCategoriaPadre(idPadre: int): List<Categoria>
    + actualizar(categoria: Categoria): boolean
    + eliminar(id: int): boolean
}
class ComponenteService {
    - componenteRepository: ComponenteRepository
    - marcaRepository: MarcaRepository
    - categoriaRepository: CategoriaRepository
    + crear(componente: Componente): Componente
    + buscarPorId(id: int): Componente
    + listarTodos(): List<Componente>
    + buscarPorMarca(idMarca: int): List<Componente>
    + buscarPorCategoria(idCategoria: int): List<Componente>
    + actualizar(componente: Componente): boolean
    + cambiarEstado(id: int, estado: String): boolean
    + eliminar(id: int): boolean
}


class VehiculoService {
    - vehiculoRepository: VehiculoRepository
    - marcaRepository: MarcaRepository
    + crear(vehiculo: Vehiculo): Vehiculo
    + buscarPorId(id: int): Vehiculo
    + listarTodos(): List<Vehiculo>
    + buscarPorMarca(idMarca: int): List<Vehiculo>
    + actualizar(vehiculo: Vehiculo): boolean
    + eliminar(id: int): boolean
}

class CompatibilidadService {
    - compatibilidadRepository: CompatibilidadRepository
    - componenteRepository: ComponenteRepository
    - vehiculoRepository: VehiculoRepository
    + crear(compatibilidad: Compatibilidad): Compatibilidad
    + buscarPorId(id: int): Compatibilidad
    + listarTodos(): List<Compatibilidad>
    + buscarPorVehiculo(idVehiculo: int): List<Compatibilidad>
    + buscarPorComponente(idComponente: int): List<Compatibilidad>
    + eliminar(id: int): boolean
}

class AlmacenService {
    - almacenRepository: AlmacenRepository
    - empresaRepository: EmpresaRepository
    - proveedorRepository: ProveedorRepository
    - direccionRepository: DireccionRepository
    + crear(almacen: Almacen): Almacen
    + buscarPorId(id: int): Almacen
    + listarTodos(): List<Almacen>
    + buscarPorEmpresa(idEmpresa: int): List<Almacen>
    + buscarPorProveedor(idProveedor: int): List<Almacen>
    + actualizar(almacen: Almacen): boolean
    + cambiarEstado(id: int, estado: String): boolean
    + eliminar(id: int): boolean
}
class InventarioService {
    - inventarioRepository: InventarioRepository
    - almacenRepository: AlmacenRepository
    - componenteRepository: ComponenteRepository
    + registrar(inventario: Inventario): Inventario
    + buscarPorId(id: int): Inventario
    + listarTodos(): List<Inventario>
    + buscarPorAlmacen(idAlmacen: int): List<Inventario>
    + buscarPorComponente(idComponente: int): List<Inventario>
    + ajustarStock(id: int, cantidad: int): boolean
    + consultarStock(idAlmacen: int, idComponente: int): int
    + eliminar(id: int): boolean
}
class CompraService {
    - compraRepository: CompraRepository
    - proveedorRepository: ProveedorRepository
    - almacenRepository: AlmacenRepository
    - usuarioRepository: UsuarioRepository
    + registrar(compra: Compra): Compra
    + buscarPorId(id: int): Compra
    + listarTodos(): List<Compra>
    + buscarPorProveedor(idProveedor: int): List<Compra>
    + cambiarEstado(id: int, estado: String): boolean
    + calcularTotal(idCompra: int): BigDecimal
    + eliminar(id: int): boolean
}
class DetalleCompraService {
    - detalleCompraRepository: DetalleCompraRepository
    - compraRepository: CompraRepository
    - componenteRepository: ComponenteRepository
    + agregar(detalle: DetalleCompra): DetalleCompra
    + buscarPorId(id: int): DetalleCompra
    + listarTodos(): List<DetalleCompra>
    + buscarPorCompra(idCompra: int): List<DetalleCompra>
    + actualizar(detalle: DetalleCompra): boolean
    + eliminar(id: int): boolean
}

class ServicioService {
    - servicioRepository: ServicioRepository
    - tallerRepository: TallerRepository
    + crear(servicio: Servicio): Servicio
    + buscarPorId(id: int): Servicio
    + listarTodos(): List<Servicio>
    + buscarPorTaller(idTaller: int): List<Servicio>
    + actualizar(servicio: Servicio): boolean
    + cambiarDisponibilidad(id: int, disponible: boolean): boolean
    + eliminar(id: int): boolean
}

class MetodoPagoService {
    - metodoPagoRepository: MetodoPagoRepository
    + crear(metodo: MetodoPago): MetodoPago
    + buscarPorId(id: int): MetodoPago
    + listarTodos(): List<MetodoPago>
    + actualizar(metodo: MetodoPago): boolean
    + cambiarEstado(id: int, activo: boolean): boolean
    + eliminar(id: int): boolean
}
class TransaccionService {
    - transaccionRepository: TransaccionRepository
    - usuarioRepository: UsuarioRepository
    - empleadoRepository: EmpleadoRepository
    - sucursalRepository: SucursalRepository
    + registrar(transaccion: Transaccion): Transaccion
    + buscarPorId(id: int): Transaccion
    + listarTodos(): List<Transaccion>
    + buscarPorUsuario(idUsuario: int): List<Transaccion>
    + buscarPorSucursal(idSucursal: int): List<Transaccion>
    + calcularTotal(id: int): BigDecimal
    + cambiarEstado(id: int, estado: String): boolean
    + cancelar(id: int): boolean
}
class DetalleTransaccionService {
    - detalleTransaccionRepository: DetalleTransaccionRepository
    - transaccionRepository: TransaccionRepository
    - inventarioService: InventarioService
    - componenteRepository: ComponenteRepository
    + agregar(detalle: DetalleTransaccion): DetalleTransaccion
    + buscarPorId(id: int): DetalleTransaccion
    + listarTodos(): List<DetalleTransaccion>
    + buscarPorTransaccion(idTransaccion: int): List<DetalleTransaccion>
    + calcularSubtotal(detalle: DetalleTransaccion): BigDecimal
    + eliminar(id: int): boolean
}
class DetalleServicioService {
    - detalleServicioRepository: DetalleServicioRepository
    - transaccionRepository: TransaccionRepository
    - servicioRepository: ServicioRepository
    + agregar(detalle: DetalleServicio): DetalleServicio
    + buscarPorId(id: int): DetalleServicio
    + listarTodos(): List<DetalleServicio>
    + buscarPorTransaccion(idTransaccion: int): List<DetalleServicio>
    + programar(id: int, fecha: LocalDateTime): boolean
    + cambiarEstado(id: int, estado: String): boolean
    + eliminar(id: int): boolean
}
class PagoService {
    - pagoRepository: PagoRepository
    - transaccionRepository: TransaccionRepository
    - metodoPagoRepository: MetodoPagoRepository
    + registrar(pago: Pago): Pago
    + buscarPorId(id: int): Pago
    + listarTodos(): List<Pago>
    + buscarPorTransaccion(idTransaccion: int): List<Pago>
    + calcularTotalPagado(idTransaccion: int): BigDecimal
    + cambiarEstado(id: int, estado: String): boolean
    + eliminar(id: int): boolean
}

class EnvioService {
    - envioRepository: EnvioRepository
    - transaccionRepository: TransaccionRepository
    - direccionRepository: DireccionRepository
    + crear(envio: Envio): Envio
    + buscarPorId(id: int): Envio
    + buscarPorTransaccion(idTransaccion: int): Envio
    + listarTodos(): List<Envio>
    + registrarEnvio(id: int, fecha: LocalDate): boolean
    + registrarRecepcion(id: int, fecha: LocalDate): boolean
    + cambiarEstado(id: int, estado: String): boolean
    + eliminar(id: int): boolean
}


class MovimientoInventarioService {
    - movimientoInventarioRepository: MovimientoInventarioRepository
    - almacenRepository: AlmacenRepository
    - usuarioRepository: UsuarioRepository
    + registrar(movimiento: MovimientoInventario): MovimientoInventario
    + buscarPorId(id: int): MovimientoInventario
    + listarTodos(): List<MovimientoInventario>
    + buscarPorAlmacen(idAlmacen: int): List<MovimientoInventario>
    + cambiarEstado(id: int, estado: String): boolean
    + eliminar(id: int): boolean
}

class DetalleMovimientoService {
    - detalleMovimientoRepository: DetalleMovimientoRepository
    - movimientoInventarioRepository: MovimientoInventarioRepository
    - inventarioService: InventarioService
    + agregar(detalle: DetalleMovimiento): DetalleMovimiento
    + buscarPorId(id: int): DetalleMovimiento
    + listarTodos(): List<DetalleMovimiento>
    + buscarPorMovimiento(idMovimiento: int): List<DetalleMovimiento>
    + aplicarMovimiento(id: int): boolean
    + eliminar(id: int): boolean
}

DepartamentoService --> DepartamentoRepository
DepartamentoService --> Departamento

MunicipioService --> MunicipioRepository
MunicipioService --> DepartamentoRepository
MunicipioService --> Municipio

ComunaService --> ComunaRepository
ComunaService --> MunicipioRepository
ComunaService --> Comuna

BarrioService --> BarrioRepository
BarrioService -->  MunicipioRepository
BarrioService -->   ComunaRepository
BarrioService --> Barrio

DireccionService --> DireccionRepository
DireccionService --> BarrioRepository
DireccionService --> Direccion

DireccionUsuarioService --> DireccionUsuarioRepository
DireccionUsuarioService -->  UsuarioRepository
DireccionUsuarioService --> DireccionRepository
DireccionUsuarioService --> DireccionUsuario

UsuarioService --> UsuarioRepository
UsuarioService --> Usuario


EmpresaService --> EmpresaRepository
EmpresaService --> Empresa

SucursalService --> SucursalRepository
SucursalService --> EmpresaRepository
SucursalService --> DireccionRepository
SucursalService --> Sucursal

SocioService --> SocioRepository
SocioService --> Socio


TarifaService --> TarifaRepository
TarifaService --> Tarifa

AfiliacionService --> AfiliacionRepository
AfiliacionService --> SocioRepository
AfiliacionService --> TarifaRepository
AfiliacionService --> Afiliacion

MarcaService --> MarcaRepository
MarcaService --> Marca

CategoriaService --> CategoriaRepository
CategoriaService --> Categoria

ComponenteService --> ComponenteRepository
ComponenteService --> MarcaRepository
ComponenteService --> CategoriaRepository
ComponenteService --> Componente


VehiculoService --> VehiculoRepository
VehiculoService -->MarcaRepository
VehiculoService --> Vehiculo





CompatibilidadService --> CompatibilidadRepository
CompatibilidadService --> ComponenteRepository
CompatibilidadService --> VehiculoRepository
CompatibilidadService --> Compatibilidad

AlmacenService --> AlmacenRepository
AlmacenService --> EmpresaRepository
AlmacenService --> SocioRepository
AlmacenService --> DireccionRepository
AlmacenService --> Almacen

InventarioService --> InventarioRepository
InventarioService --> AlmacenRepository
InventarioService --> ComponenteRepository
InventarioService --> Inventario

CompraService --> CompraRepository
CompraService --> SocioRepository
CompraService --> AlmacenRepository
CompraService --> UsuarioRepository
CompraService --> Compra

DetalleCompraService --> DetalleCompraRepository
DetalleCompraService --> MovimientoInventarioRepository
DetalleCompraService --> InventarioService
DetalleCompraService --> DetalleCompra

ServicioService --> ServicioRepository
ServicioService --> SocioRepository
ServicioService --> Servicio

MetodoPagoService --> MetodoPagoRepository
MetodoPagoService --> MetodoPago

TransaccionService --> TransaccionRepository
TransaccionService --> UsuarioRepository
TransaccionService --> SucursalRepository
TransaccionService --> Transaccion

DetalleTransaccionService --> DetalleTransaccionRepository
DetalleTransaccionService --> TransaccionRepository
DetalleTransaccionService --> InventarioRepository
DetalleTransaccionService --> ComponenteRepository
DetalleTransaccionService --> DetalleTransaccion

DetalleServicioService --> DetalleServicioRepository
DetalleServicioService --> TransaccionRepository
DetalleServicioService --> ServicioRepository
DetalleServicioService --> DetalleServicio

PagoService --> PagoRepository
PagoService --> TransaccionRepository
PagoService --> MetodoPagoRepository
PagoService --> Pago

EnvioService --> EnvioRepository
EnvioService --> TransaccionRepository
EnvioService --> Envio

MovimientoInventarioService --> MovimientoInventarioRepository
MovimientoInventarioService --> AlmacenRepository
MovimientoInventarioService --> UsuarioRepository
MovimientoInventarioService --> MovimientoInventario

DetalleMovimientoService --> DetalleMovimientoRepository
DetalleMovimientoService --> MovimientoInventarioRepository
DetalleMovimientoService --> InventarioService
DetalleMovimientoService --> DetalleMovimiento


MenuGeografia
MenuUsuarios
MenuEmpresa
MenuSocios
MenuCatalogo
MenuVehiculos
MenuInventario
MenuCompras
MenuVentas
MenuServicios


Main --> Menu

Menu --> MenuGeografia
MenuGeografia --> DepartamentoService
MenuGeografia --> MunicipioService
MenuGeografia --> ComunaService
MenuGeografia --> BarrioService
MenuGeografia --> DireccionService
MenuGeografia --> DireccionUsuarioService

Menu --> MenuUsuarios
MenuUsuarios --> UsuarioService


Menu --> MenuEmpresa
MenuEmpresa --> EmpresaService
MenuEmpresa --> SucursalService

Menu --> MenuSocios
MenuSocios --> SocioService
MenuSocios --> AfiliacionService

Menu --> MenuCatalogo
MenuCatalogo --> MarcaService
MenuCatalogo --> CategoriaService
MenuCatalogo --> ComponenteService

Menu --> MenuVehiculos
MenuVehiculos --> VehiculoService
MenuVehiculos --> CompatibilidadService

Menu --> MenuInventario
MenuInventario --> AlmacenService
MenuInventario --> InventarioService
MenuInventario --> MovimientoInventarioService
MenuInventario --> DetalleMovimientoService

Menu --> MenuCompras
MenuCompras --> CompraService
MenuCompras --> DetalleCompraService

Menu --> MenuVentas
MenuVentas --> TransaccionService
MenuVentas --> DetalleTransaccionService
MenuVentas --> PagoService
MenuVentas --> MetodoPagoService
MenuVentas --> EnvioService

Menu --> MenuServicios
MenuServicios --> ServicioService
MenuServicios --> DetalleServicioService

```
