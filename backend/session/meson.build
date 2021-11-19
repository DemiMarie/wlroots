session = get_option('session')
if not session.disabled()
	libseat = dependency('libseat',
		version: '>=0.2.0',
		fallback: ['seatd', 'libseat'],
		default_options: ['server=disabled', 'man-pages=disabled'],
		required: session.enabled()
	)
	if libseat.found()
		wlr_files += files('session.c')
		wlr_deps += libseat
		features += { 'session': true }
	endif
endif
