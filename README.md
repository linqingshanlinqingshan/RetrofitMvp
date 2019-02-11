# RetrofitMvp
## 项目框架：retrofit2 + okhttp3 + rxjava2 + evenbus

### 异步获取数据
        Api.getDefault().getShopBrandAdver()
                .compose(RxHelper.<ShopBrandAdverBean>handleResult())
                .subscribe(new RxObserver<ShopBrandAdverBean>((Activity) mView) {
                    @Override
                    public void _onNext(ShopBrandAdverBean shopBrandAdverBean) {
                        if (shopBrandAdverBean != null) {
                            List<ShopBrandAdverBean.DataBean> data = shopBrandAdverBean.getData();
                            mView.refreshView(data, name, password);
                        }

                    }

                    @Override
                    public String _onMessage() {
                        return null;
                    }

                    @Override
                    public void _onError() {

                    }
                });

### 动态权限监测
        new RxPermissions(this)
                .request(Manifest.permission.CAMERA, Manifest.permission.WRITE_EXTERNAL_STORAGE)
                .subscribe(new Consumer<Boolean>() {
                    @Override
                    public void accept(@io.reactivex.annotations.NonNull Boolean aBoolean) throws Exception {
                        if (!aBoolean) {
                            Toast.makeText(MainActivity.this, "请您先允许权限！", Toast.LENGTH_SHORT).show();
                            return;
                        } else {
                            startActivity(new Intent(MainActivity.this, LoginActivity.class));
                        }
                    }
                });
