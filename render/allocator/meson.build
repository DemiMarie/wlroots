wlr_files += files('allocator.c')

all_allocators = ['drm-dumb', 'gbm', 'shm']
allocators = get_option('allocators')
if 'auto' in allocators and get_option('auto_features').enabled()
	allocators = all_allocators
elif 'auto' in allocators and get_option('auto_features').disabled()
	allocators = []
endif

if 'shm' in allocators
	wlr_files += files('shm.c')
	features += {'shm-allocator': true}
endif

if 'gbm' in allocators
	gbm = dependency('gbm', version: '>=17.1.0')
	wlr_files += files('gbm.c')
	wlr_deps += [gbm]
	has = cc.has_function('gbm_bo_get_fd_for_plane', dependencies: [gbm])
	add_project_arguments('-DHAS_GBM_BO_GET_FD_FOR_PLANE=@0@'.format(has.to_int()), language: 'c')
	features += {'gbm-allocator': true}
endif

if 'drm-dumb' in allocators
	features += {'drm-dumb-allocator': true}
	wlr_files += files('drm_dumb.c')
endif
