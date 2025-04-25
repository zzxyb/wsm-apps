project(
	'wsm-apps',
	'c',
	version: '0.19.0-dev',
	license: 'MIT',
	meson_version: '>=1.3',
	default_options: [
		'c_std=' + (meson.version().version_compare('>=1.4.0') ? 'c23,c11' : 'c11'),
		'warning_level=2',
		'werror=true',
	],
)

add_project_arguments([
	'-D_POSIX_C_SOURCE=200809L',
], language: 'c')

cc = meson.get_compiler('c')

add_project_arguments(cc.get_supported_arguments([
	'-Wundef',
	'-Wlogical-op',
	'-Wmissing-include-dirs',
	'-Wold-style-definition',
	'-Wpointer-arith',
	'-Winit-self',
	'-Wstrict-prototypes',
	'-Wimplicit-fallthrough=2',
	'-Wendif-labels',
	'-Wstrict-aliasing=2',
	'-Woverflow',
	'-Wmissing-prototypes',
	'-Walloca',

	'-Wno-missing-braces',
	'-Wno-missing-field-initializers',
	'-Wno-unused-parameter',
]), language: 'c')

wayland_client = dependency('wayland-client')
wayland_cursor = dependency('wayland-cursor')
wayland_egl = dependency('wayland-egl')
wayland_protos = dependency('wayland-protocols', version: '>=1.24')

examples = {
	'brightness': {
		'src': [
			'brightness/main.c',
			'brightness/wsm_brightness.c'
		],
		'dep': [wayland_protos],
	},
}

foreach name, element : examples
	executable(
		name,
		element.get('src', []),
		dependencies: [wayland_client, element.get('dep', [])],
	)
endforeach
