# RetrofitMvp
## retrofit2 + okhttp3 + rxjava2 + evenbus

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
